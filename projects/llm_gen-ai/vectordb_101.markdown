---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Vector Databases - 101
parent: LLM and Gen-AI
permalink: /llm_genai/vectordb
nav_order: 102
---

# Vector Databases - 101
Vector Database
{: .badge .badge-pill .badge-primary }
LLM
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

# Traditional Search vs Semantic Search
  - traditional search understands words, but it doesn't understand their meaning. 
  - It simply compares text. 
  - This approach works well for exact keyword matching but struggles when different words have similar meanings. 

# Semantic Search
  - Semantic search works differently from compare text approach. Instead of matching words, it tries to understand the meaning behind the user's query. 
  - Semantic search recognizes that: car, automobile, vehicle are closely related. Similarly, maintain, service, repair also have similar meanings.
  - Because semantic search understands meaning, it returns much more relevant results. This is exactly why modern AI search systems feel much smarter than traditional keyword search. 

# Vector Databases
  - a Storage to stores the Embedding data / vector (which are mathematical representations of meaning) in vector data type.
  - Powerful to solving semantic queries, ask about similarity and relation.
  - This DB acts as memory to get the data for LLM Model.
  - Why not use a normal database:
    - Relational databases are optimized for exact matching, sorting, filtering, and transactional operations. 
    - They are not designed to perform high-speed similarity searches across millions of high-dimensional vectors. 
    - Vector databases use specialized indexing algorithms that make similarity search incredibly fast.

## Vector Space
  - Like a plotting cities on a map, Embeddings work in a similar way. Instead of physical locations, each sentence occupies a position inside a mathematical space called `vector space`.
  - In this space:
    - Sentences with similar meanings are located close together. 
    - Sentences with different meanings are farther apart. 

# Embedding
  - An embedding is a numerical representation of data. 
  - Instead of storing text as words, an AI model converts the text into a long list of numbers.
  - These numbers capture the meaning of the sentence. 
  - This numerical representation is called an embedding vector. Two sentences with similar meanings produce vectors that are close together. Two unrelated sentences produce vectors that are farther apart. This is the key idea behind semantic search.

## Embedding Flow
  - <img src="/assets/images/llm_genai/vector_01.webp" alt="drawing" width="500"/>

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
  - Recommendataion engines
  - AI agents with memory
  - Document QA
  - Similarity matching
  - Fraud detection
  - Image and audio search
  - Enterprise Knowledge Bases

## Vector DB tools
  - Dedicated DB Examples:
    - Chroma
    - LanceDB
    - Milvus
    - Weaviate
    - Pinecone
  - DS Support vector search:
    - PostgreSQL (pgvector)
    - Cassandra
    - ClickHouse
    - OpenSearch
    - elasticsearch
    - Redis
