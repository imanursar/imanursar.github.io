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


# Vector Databases
  - a Storage to stores the Embedding data (which are mathematical representations of meaning) in vector data type.
  - Powerful to solving semantic queries, ask about similarity and relation.
  - This DB acts as memory to get the data for LLM Model.

## Embedding Flow
  - <img src="/assets/images/llm_genai/vector_01.webp" alt="drawing" width="500"/>

## Techical
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

## Vector DB Usage
  - Semantic Search
  - Recommendataion engines
  - AI agents with memory
  - Document QA
  - Similarity matching
  - Fraud detection
  - Image and audio search

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
