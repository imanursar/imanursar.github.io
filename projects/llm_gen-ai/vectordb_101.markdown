---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Vector Databases - 101
parent: LLM and Gen-AI
permalink: /llm_genai/vectordb
nav_order: 102
mermaid: true
---

# Vector Databases - 101
Vector Database
{: .badge .badge-pill .badge-primary }
LLM
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

# Vector Databases
  - a Storage to stores the Embedding data / vector (which are mathematical representations of meaning) in vector data type or multi-dimensional space to perform high-eﬃcient queries based on similarity.
  - Powerful to solving semantic queries, ask about similarity and relation.
  - This DB acts as memory to get the data for LLM Model.

## Overview
  - <img src="/assets/images/llm_genai/vector/vector_06.webp" alt="drawing" />

  - <img src="/assets/images/llm_genai/vector/vector_07.webp" alt="drawing" />

  - <img src="/assets/images/llm_genai/vector/vector_08.webp" alt="drawing" />
  
  - <img src="/assets/images/llm_genai/vector/vector_09.webp" alt="drawing" />

## Vector Space
  - Vector is a quantity, such as velocity, completely specified by a magnitude and a direction.
  - Like a plotting cities on a map, Embeddings work in a similar way. Instead of physical locations, each sentence occupies a position inside a mathematical space called `vector space`.
  - In this space:
    - Sentences with similar meanings are located close together. 
    - Sentences with different meanings are farther apart. 

  - <img src="/assets/images/llm_genai/vector/vector_01.webp" alt="drawing" />
  
  - <img src="/assets/images/llm_genai/vector/vector_10.webp" alt="drawing" />

## Why are Vectors Used in a Vector Database?
  - Data `shows up` in the world or 80% or more of data is unstructured.
  - Efficient Representation of Complex Data
    - Dimensionality - representing data in high-dimensional space
    - Uniformity - data can be converted into a uniform format (numerical vectors)
  - Enabling Similarity Search
  - Leveraging Machine Learning Models
  - Optimizing Performance and Scalability
  - Improving User Experience
    - Real-time interaction (recommendations, search results or data analysis outputs)

## Why not use a normal database:
  - Relational databases are optimized for exact matching, sorting, filtering, and transactional operations. 
  - They are not designed to perform high-speed similarity searches across millions of high-dimensional vectors. 
  - Vector databases use specialized indexing algorithms that make similarity search incredibly fast.

## Traditional Database vs Vector Database
### RMDBS
  - **Structured data**: predefined columns and rows
  - **Schema-based**: database structure must be defined before hand.
  - **Data manipulation and querying**: manipulation through SQL
  - **ACID Compliant**: Atomic, Consistency, Isolation, Durability
  - **Indexing**: to speed up data retrieval
  
  - How data search works in traditional databases
    - <img src="/assets/images/llm_genai/vector/vector_03.webp" alt="drawing" />
  
  - Limitation
    - Scalability: hard to deal with complex queries across large tables
    - Flexibility: changing DB’s schema can be disruptive
    - Handling Unstructured Data: not well-suited for handling unstructured data (images, text, audio, video)

### Vector Database
  - **Data Representation as Vectors**: vector is vectorized which brings lots of benefits for searching
  - **Similarity Search**: finding data points closest to a given query vector.
  - **Efficiency in High-Dimensional Searches**: use of specialized indexing structures that are highly optimized
  - **Handling Unstructured Data**: vector database are made to deal with unstructured data
  - **Schema-less Design**: don’t require schema - allowing more ﬂexibility in handling various data types and  structures

# Embedding
  - An embedding is a numerical representation of data. 
  - Embeddings  are vectors that encodes semantic similarities between the items they represent.
  - Instead of storing text as words, an AI model converts the text into a long list of numbers.
  - These numbers capture the meaning of the sentence. 
  - This numerical representation is called an embedding vector. Two sentences with similar meanings produce vectors that are close together. Two unrelated sentences produce vectors that are farther apart. This is the key idea behind semantic search.

  <img src="/assets/images/llm_genai/vector/vector_04.webp" alt="drawing" />

  - Text with similar content and meaning will have similar vectors

  <img src="/assets/images/llm_genai/vector/vector_05.webp" alt="drawing" />

## Embedding Flow
  - <img src="/assets/images/llm_genai/vector/vector_01.webp" alt="drawing" />

## Embedding Dimensions

  | Model                  | Dimensions |
  | ---------------------- | ---------- |
  | text-embedding-3-small | 1536 dim   |
  | text-embedding-3-large | 3072 dim   |
  | Gemini embedding       | 768 dim    |
  | BGE-small              | 384 dim    |

  | Dimensions | Storage | Speed  | Nuance |
  | ---------- | ------- | ------ | ------ |
  | 384        | Low ↓   | Fast ↑ | Good   |
  | 768        | Med     | Med    | Better |
  | 1536       | High ↑  | Slow ↓ | Best   |

# Traditional Search vs Semantic Search
  - traditional search understands words, but it doesn't understand their meaning. 
  - It simply compares text. 
  - This approach works well for exact keyword matching but struggles when different words have similar meanings. 

## Semantic Search
  - Semantic search works differently from compare text approach. Instead of matching words, it tries to understand the meaning behind the user's query. 
  - Semantic search recognizes that: car, automobile, vehicle are closely related. Similarly, maintain, service, repair also have similar meanings.
  - Because semantic search understands meaning, it returns much more relevant results. This is exactly why modern AI search systems feel much smarter than traditional keyword search. 

# Techical
  - **Stores**
    - Vectors
    - Metadata
    - Original content
  - **Supports**
    - Fast similarity search
    - Filtering
    - Scalable retrieval
  - **Indexing**
    - Inverted Indexes
    - K-d Trees
    - Priority Queues
    - Local Sensitive Hashing (LSH): Similar vectors have higher chances of sharing similar hash codes.
    - Hierarchical Navigable Small World (HNSW): Organize vectors into difference layers with varying probabilities into a hierarchical graph structure. 
    - Approximate Nearest Neighbor Oh Yeah (ANNOY): Organize high-dimensional data using binary tree.
  - **Measure similarity with distance function**
    - Cosine similarity
    - Euclidean distance
    - Dot product
    - Scoring hybrid system
    - vector_score * 0.7 + keyword_score * 0.3

## Measuring Similarity
  - Once text has been converted into vectors, comparing two pieces of text becomes a mathematical problem. 
  - Instead of comparing words, we compare vectors. 
  - One of the most common techniques is called Cosine Similarity.  Cosine Similarity measures how similar two vectors are. If two vectors point in nearly the same direction, they are considered highly similar. If they point in different directions, they are less similar. 

## Cost of Vector DB
  - Large storage for storing vectors
  - RAM heavy
  - Indexing is complex

## Core Architecture of a Vector Database
  - Ingestion Layer - Consume the data
    - Raw data
    - Vectors
    - Metadata
  - Indexing Layer - Build Appoximate Nearest Neighbor (ANN) indexes. Using Graph and clustering to indexing.
    - HNSW
    - IVF
    - PQ
  - Storage Layer
    - Vectors
    - Metadata
    - IDs
  - Query Engine
    - A vector
    - Filters
    - Top K
    - return most similar items

## ELI5: Sparse Vector vs Dense Vector
  - e.g. we have a huge sentence with 100000 words
  - **Sparse Vector**
    - We create a list with 100,000 slots.

      ```
        Slot #523 = "love" → 1
        Slot #1829 = "pizza" → 1
        Slot #7321 = "I" → 1
        Everything else = 0
      ```

    - Result: [0,0,0,0,1,0,0,0,0,0,...,1,...,1,...]
    - Most values are zero. That's why it's called **sparse** (mostly empty) and only exact overlapping terms contribute.
    - Sparse vectors are usually generated by algorithms like:
      - TF-IDF
      - BM25
  
  - **Dense Vector**
    - Instead of storing every word position, an AI model converts the sentence into something like:
    
    ```
      [0.24, -0.87, 0.56, 0.13, ...]
    ```
    - Maybe only 768 numbers long. These numbers don't correspond to specific words. Instead they capture the meaning of the sentence.
    - Sentence with similar sentence will produce vectors that are close together. That's why it's called **dense** (almost every dimension contains information).

  | Feature                | Sparse Vector              | Dense Vector                 |
  | ---------------------- | -------------------------- | ---------------------------- |
  | Representation         | Mostly zeros               | Mostly non-zero              |
  | Dimensions             | Very high (100k+)          | Lower (384–4096)             |
  | Captures meaning       | No/limited                 | Yes                          |
  | Exact keyword matching | Excellent                  | Moderate                     |
  | Synonym handling       | Poor                       | Excellent                    |
  | Explainability         | High                       | Low                          |
  | Storage efficiency     | Sparse compression         | Fixed-size vectors           |
  | Best for               | Search engines, IDs, codes | Semantic search, RAG         |
  | Typical algorithm      | BM25, TF-IDF, SPLADE       | Embeddings from transformers |
  | Modern usage           | Hybrid search              | Hybrid search                |

## BM25 or Best Match 25
  - Technic to search by frequency methods.
  - BM25 scores a document against a query by looking at it from multiple directions. Its main components are:
    - TF term frequency component: asks how often the term appears in this specific document. BM25 applies a saturation function rather than just using the raw frequency. Because of this saturation function the score grows rapidly in the starting and then flattens.
    - IDF component: how difficult it is to find a term anywhere in the corpus. IDF gives rare terms more weightage. 
    - The length normalisation component penalises longer documents. A longer document naturally contains more term occurrences.
  - It is a bag-of-words model and word order and semantics do not matter to it.

## Vector DB Usage
  - Semantic Search
  - Recommendation engines
  - AI agents with memory
  - Document QA
  - Similarity matching
  - Fraud detection
  - Image and audio Retrieval & Similarity search
  - Enterprise Knowledge Bases
  - Bioinformatics

## Vector DB tools
  - Dedicated DB Examples:
    - ChromaDB
    - LanceDB
    - Milvus
    - Weaviate
    - Pinecone
  - DB Support vector search:
    - PostgreSQL (pgvector)
    - Cassandra
    - ClickHouse
    - OpenSearch
    - elasticsearch
    - Redis
  
   Outer pipes Cell padding

  | DATABASE | BEST FOR                                               | PRICING                            | SELF-HOST | Tier              |
  | -------- | ------------------------------------------------------ | ---------------------------------- | --------- | ----------------- |
  | pgvector | PostgreSQL Users, Hybrid Search, Simple Use Cases      | Free (Open Source) or Cloud        | ✔         |Enterpise Standard |
  | Pinecone | Managed Service, Scalability, Ease of Use              | Tiered (Usage-based) / Free Tier   | ❌        |Managed Vector DB  |
  | Chroma   | Local Development, Python Ecosystem, Rapid Prototyping | Free (Open Source) / Cloud (Soon)  | ✔         |Local dev Vector DB|
  | Qdrant   | High Performance, Rust-based, Filtering & Search       | Free (Open Source) / Cloud Managed | ✔         |Rising star        |
  | Weaviate | GraphQL, Modules (ML models), Production-ready         | Free (Open Source) / Cloud Managed | ✔         |Rising star        |
  | Milvus   | Large-scale Deployments, High Throughput, Feature-rich | Free (Open Source) / Cloud Managed | ✔         |Rising star        |

## Vector DB Decision Framework

  ```mermaid
  flowchart TD;
      A[Prototyping?]-->B[Have Postgres?];
      A[Prototyping?]-->D[Chroma DB];
      B[Have Postgres?]-->C[Want managed?];
      B[Have Postgres?]-->E[pgvector];
      C[Want managed?]-->F[Pinecone];
      C[Want managed?]-->G[Qdrant];
  ```

