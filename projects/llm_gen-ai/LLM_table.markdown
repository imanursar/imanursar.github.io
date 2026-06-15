---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: LLM Chat with Database Data
parent: LLM and Gen-AI
permalink: /llm_genai/llm_table
nav_order: 105
---

# LLM Chat with Database Data
LLM
{: .badge .badge-pill .badge-primary }
table
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

Self-hosted AI interface for LLMs, Agentic AI, and internal data. Fully offline, customizable, and capable of translating user queries into database searches and summaries automatically.

# Schema

  {% include whimsical.html src="https://whimsical.com/embed/EaVTkCZnTn61tmXHzVd2Xm@8ADn3nfZACau2b3hPSkvEwp2yX9RgCoh91Sy" %}

# Video

  {% include video.html src="/assets/videos/ask_the_database.mp4" %}


# Text to SQL
  - A typical usage scenario of using Al to improve productivity
  - Use SQL to query data from relational databases
  - Understand structures of database tables
  - SQL is not easy for non-technical people to learn
  - Use natural language to describe query requirements 
  - Use LLM to generate SQL statements from user input

# Basic concepts
  - Leverage the capability of LLM directly
  - Generate code using LLM
  - LLM requires database metadata
  - Metadata of database tables and columns
  - Include database metadata in prompts sent to LLM

# Example prompt
  
  ```
  You are a Postgres expert. Generate SQL statements to answer user's query. Output the SQL only. Don't use Markdown format.

  The table name is netflix_shows. Column names and data types are shown as below: show_id, text; type, text; title, text; director, text; cast_members, text; country, text; date_added, date; release_year, int4; rating, text; duration, text; listed_in, text; description, text.

  {user_input}
  ```

# Database Metadata
  - Using handwritten database metadata is not a good choice
  - Use JDBC API to get database metadata
  - Database metadata:
    - Metadata of all tables
    - Table metadata
      - Name, description, catalog, schema
    - Column metadata
      - Name, description, data type
  - Include database metadata as system text of a prompt
  - The limitation on context window of LLM compare to number of table and columns used.
  - This Database metadata can be store in VectorDB with such schema:
    - ID
    - Content
    - Collection of media
    - Map of metadata
    - Embedding

# Low Cadinality Values
  - Columns with a small categories could be implemented as enum values. This will be include in `WHERE` clause of SQL statement.
  - We can use `SELECT DISTINCT` for a given column.
  - Chose a threshold of number of unique values.

