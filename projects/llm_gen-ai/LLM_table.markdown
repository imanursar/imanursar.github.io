---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: LLM Chat with Database Data
parent: LLM and Gen-AI
permalink: /llm_genai/llm_table
nav_order: 105
---

# Self-Hosted Agentic AI Platform for Natural Language Database Interaction
LLM
{: .badge .badge-pill .badge-primary }
table
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

Self-hosted AI interface for LLMs, Agentic AI, and internal data. Fully offline, customizable, and capable of translating user queries into database searches and summaries automatically.

# Schema

  {% include whimsical.html src="https://whimsical.com/embed/EaVTkCZnTn61tmXHzVd2Xm@8ADn3nfZACauTPwJSrBC82Q8Gb3hvmoyXfNR" %}


# Video

  {% include video.html src="/assets/videos/ask_the_database.mp4" %}


# Self-Hosted AI Interface for LLM, Agentic AI, and Internal Data

Develop a self-hosted AI interface that combines Large Language Models (LLM), Agentic AI workflows, and internal enterprise data sources into a single intelligent assistant platform. The system is designed to operate fully offline, allowing organizations to interact with internal databases while maintaining full control over their data and infrastructure.

Enable users to communicate with internal data using natural language instead of writing complex database queries manually. The platform translates user questions into executable database operations, retrieves the required information, and generates human-readable summaries using local LLM inference.

Customize the AI workflow based on organizational requirements by controlling the models, prompts, database connectors, and execution logic. This architecture transforms traditional database interaction into an AI-powered analytical experience.

## Modular System Architecture

Separate the platform into three independent modules: Internal Database Module, AI Agent Module, and Query Processor Module.

Design each module with a specific responsibility to improve maintainability, scalability, and operational flexibility. The Internal Database Module manages data access and database communication. The AI Agent Module handles reasoning, query generation, validation, execution, and result interpretation. The Query Processor Module manages user interaction and final response generation.

Running each module independently allows the system to scale individual components based on workload requirements and prevents tight dependency between data storage, AI processing, and user interaction layers.

# Internal Database Module
## Internal Database Management and Data Access Layer

Build the Internal Database Module as the foundation layer that stores organizational data together with its metadata information. This module acts as the source of truth for the AI system and provides controlled access to structured enterprise information.

Store both operational data and supporting metadata, including database schema information, table relationships, column definitions, descriptions, and other contextual information required by the AI Agent.

Provide a Database Adaptor as the communication layer between the AI Agent and the database system. The adaptor manages database connection, schema extraction, query execution, and context collection. This abstraction allows the AI Agent to interact with different database technologies without changing the core AI workflow.

The database adaptor performs several responsibilities:
- Collect database schema information
- Retrieve metadata and table descriptions
- Execute generated SQL queries
- Return query results to the AI processing layer
- Provide additional context for improving LLM understanding

# AI Agent Module
## Retrieval Process for Database Context Collection

Implement the retrieval process as the first stage inside the AI Agent workflow. This process collects required database information through the Database Adaptor before generating any query.

Retrieve relevant database context such as:
- Available tables
- Column structures
- Data types
- Relationships
- Metadata descriptions
- Existing database context

Use this information as additional context for the LLM model to understand the database structure before converting user questions into SQL commands.

The retrieval process reduces incorrect query generation by ensuring that the model generates SQL based on actual database availability rather than assumptions.

## Generator Process for Text-to-SQL Conversion

Develop the generator process to translate natural language questions into SQL queries using a local LLM model.

Combine multiple inputs before sending them to the model:
- User query
- Retrieved database information
- System prompt instructions

Use Ollama as the local inference engine to execute the LLM model and generate the Text-to-SQL output.

The system prompt guides the model to understand database rules, query requirements, and expected output format. The generated SQL query represents the translation between human language and database operations.

This process enables users to ask analytical questions naturally without requiring SQL knowledge.

## SQL Validation and Query Enhancement Process

Implement a validation layer to verify the generated SQL before executing it against the database.

The validation process checks whether the generated command follows the expected query rules, especially ensuring that the output only contains DQL (Data Query Language) operations such as SELECT statements.

Prevent unsafe database operations by blocking unwanted commands, including:

- DDL commands (CREATE, ALTER, DROP)
- DML commands (INSERT, UPDATE, DELETE)

After validation, apply query enhancement techniques to improve execution compatibility. Adjust formatting, syntax, or query structure when necessary while preserving the original user intent.

This layer acts as a safety mechanism between the LLM-generated output and the production database environment.

## Query Execution Through Database Adaptor

Execute the validated SQL query through the Database Adaptor after completing the validation process.

The adaptor sends the final SQL command to the target database and retrieves the execution result.

Return the query output back to the AI Agent pipeline as structured information. This result becomes the primary source for generating the final natural language response.

Separating execution logic through the adaptor ensures that database interaction remains controlled and independent from the LLM reasoning process.

## Result Summarization Using Local LLM

Transform raw database query results into understandable explanations by using an additional LLM summarization process.

Provide the summarization model with:
- SQL execution results
- Database context enrichment
- User query information

Use Ollama-based local LLM inference to generate a conversational response that explains the retrieved data.

The summarization process converts structured database outputs into meaningful insights, allowing users to understand results without manually analyzing tables or raw query responses.

# Query Processor Module
## User Query Processing and Context Enrichment

Process user questions through the Query Processor Module before sending them into the AI Agent workflow.

Transform the original user input using several preparation steps:
- Context Builder
- Query Enrichment
- Prompt Template

The Context Builder maintains conversation history and relevant interaction context. Query Enrichment improves the original question by adding missing information or restructuring the request.

The Prompt Template combines user input, system instructions, and available context into a structured prompt format suitable for the LLM pipeline.

The processed query becomes the main input for the retrieval and generation workflow.

## Retriever Module and Final Response Generation

Implement the retriever module as the final intelligence layer responsible for combining AI Agent outputs, query results, and summaries into a clean response.

Use a local LLM model through Ollama as the chat generation engine. Configure the model behavior using inference parameters such as:
- **n_ctx** for controlling context window size
- **temperature** for controlling response creativity
- **top_p** for controlling token selection probability

The retriever module receives:
- Optimized user prompt
- Query execution result
- Generated database summary
- System prompt instructions

The LLM then restructures the information into a final response format that is easier for users to understand.

Apply final response enhancement to remove unnecessary details, improve readability, and ensure that the generated answer remains aligned with the original user question. 

# System Objective

Build the platform as a private AI-powered data assistant that enables natural language interaction with enterprise databases.

By combining Agentic AI workflow, Text-to-SQL generation, database reasoning, and local LLM inference, the system provides a secure alternative to cloud-based AI analytics solutions.

The architecture enables:
- Offline AI deployment
- Secure internal data access
- Natural language database querying
- Automated SQL generation
- Query validation and execution control
- AI-powered data summarization

This approach allows organizations to integrate AI capabilities into existing data infrastructure while maintaining governance, privacy, and operational control.


