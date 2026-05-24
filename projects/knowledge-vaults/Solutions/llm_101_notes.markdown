---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: LLM - AI Agent 101 Notes
parent: kv - Solutions
grand_parent: Knowledge Vaults
permalink: /knowledge-vaults/solutions/llm101-notes
nav_order: 100
---

# LLM Script Notes
Solutions
{: .badge .badge-pill .badge-primary }

* Do not remove this line (it will not be displayed)
{:toc}


# Load Documents

  ```python
  from langchain.document_loaders import PyPDFLoader 
  from langchain.text_splitter import ( RecursiveCharacterTextSplitter)

  # Load a PDF
  loader = PyPDFLoader("knowledge_base.pdf") 
  documents = loader.load()
  
  # Split into overlapping chunks
  splitter = RecursiveCharacterTextSplitter(
              chunk_size=512,
              chunk_overlap=64,
              separators=["\n\n", "\n", ""]
            )
  
  chunks = splitter.split_documents(documents)
  ```

# Tokenization

  ```python
  import tiktoken
  enc = tiktoken.get_encoding("cl100k_base")
  tokens = enc.encode(text)
  ```

# Token Prediction

  ```python
  from transformers import AutoTokenizer, AutoModelForCausalLM
  
  tokenizer = AutoTokenizer.from_pretrained("gpt2") 
  model = AutoModelForCausalLM. from_pretrained ("gpt2")
  
  inputs = tokenizer("The transformer architecture", return_tensors="pt")
  
  # Greedy decoding
  greedy = model.generate(**inputs, max_new_tokens=20)
  
  # Sampling with temperature + top-p 
  sampled = model.generate(**inputs,
            max_new_tokens=20, do_sample=True,
            temperature=0.8,
            top_p=0.95,
            )
  ```

# Chuncking

  ```python
  langchain.text_splitter.CharacterTextSplitter(
      separator: str = "\n\n"
      chunk_size=4000, 
      chunk_overlap=200,
      length_function=<builtin function len>,
  )
  ```

# Embeddings
  **llama**
  ```python
  from transformers import AutoTokenizer, AutoModel
  model_id = 'meta-llama/Llama-3.2-1B'
  tokenizer = AutoTokenizer.from_pretrained(model_id)
  model = AutoModel.from_pretrained(model_id)

  inputs = tokenizer("Hello world", return_tensor='pt')
  embeds = model.embed_token(inputs['input_ids'])
  ```

  **Openai**
  ```python
  
  from langchain_openai import OpenAIEmbeddings 
  import numpy as np

  # Initialize embedding model
  embeddings = OpenAIEmbeddings(model="text-embedding-3-small")
  
  #Embed all chunks -> 1536-dim vectors 
  texts = [c.page_content for c in chunks] 
  vectors = embeddings.embed_documents(texts) 
  matrix = np.array(vectors) 
  
  print(matrix.shape)
  # -> (N_chunks, 1536)
  ```

# Vector Store

  ```python
  from langchain_community.vectorstores import FAISS 
  # Build FAISS index from chunks + embeddings 
  vectorstore = FAISS.from_documents(
                  documents-chunks, 
                  embedding=embeddings
                )

  # Persist to disk
  vectorstore.save_local("faiss_index")
  # Load back later
  vectorstore = FAISS.load_local("faiss_index", embeddings,
                allow_dangerous_deserialization=True
                )
  ```

# Retriever module

  ```python  
  # Create a retriever from the vector store 
  retriever = vectorstore.as_retriever(
                search_type="similarity", 
                search_kwargs={"k": 4}
                )
  
  query= "What is the refund policy?" 

  # Returns top 4 most relevant chunks
  relevant_docs = retriever.invoke(query) 
  for i, doc in enumerate(relevant_docs): 
    print(f" [{i+1}] score={doc.metadata}") 
    print(doc.page_content [:100])
  ```

# Answer Generation
  ```python
  from langchain_openai import ChatOpenAI
  from langchain.schema import HumanMessage, SystemMessage

  llm = ChatOpenAI(model="gpt-40-mini", temperature=0) 
  context = "\n\n".join([d.page_content for d in relevant_docs])

  messages = [
    SystemMessage(content=f"""Answer using ONLY
  this context: \n{context}
  If unsure, say 'I don't know'.
  """)
  HumanMessage(content=query)
  ]

  response = llm. invoke(messages) 
  print(response.content)
  ```

# Samples

  ```python
  import ollama

  response = ollama.chat(
              model="llama3.2",
              messages=[{'role':"user", "content":"what is backpop?"}]
              )
  print(response['message']['content'])
  ```

# RAG Chain
  **Langchain's RetrievalQA**
  ```python
  from langchain.chains import RetrievalQA 
  from langchain.prompts import PromptTemplate

  prompt = PromptTemplate(
    input_variables=["context", "question"], 
    template="""Context: \n{ context}\n
  Q: {question}\nA: """
  )

  qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever retriever,
    chain_type_kwargs={"prompt": prompt}, 
    return_source_documents=True
  )

  result = qa_chain.invoke({"query": query}) 
  print(result["result"])
  ```