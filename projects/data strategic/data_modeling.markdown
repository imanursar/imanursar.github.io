---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Data Modeling Process
parent: Data Strategic
permalink: /data strategic/data_model
nav_order: 87
---

# Data Modeling Process

data modeling
{: .badge .badge-pill .badge-primary }
data strategic
{: .badge .badge-pill .badge-secondary }


## Schema

  {% include whimsical.html src="https://whimsical.com/embed/JSC42FRTDvPy9vcbdQRpaG@or4CdLRbgroYcwcEec92b3rdgKngCnthAuk2LiDJh?color-mode=light" %}

## ELI5
  - Data Models define what data is.
  - Define how operational and analytical databases are designed.
  - Conceptual Model
    - Business view.
    - No tables.
    - No datatype.
    - Only concepts.
  - Logical Model
    - Now we define table schema
  - Physical Model
    - Now database specific.

## Main Concepts

  - The Bussiness Model
  - Conceptual Data Model
  - Logical Data Model
  - Physical Data Model 

## Comparison Table

  | Aspect               | Semantic Layer / Ontology / Context                                       | Medallion Architecture                                  | Data Models                                               |
  | -------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------- | --------------------------------------------------------- |
  | Primary question     | What does the data mean?                                                  | How does the data flow and improve?                     | How is the data structured?                               |
  | Focus                | Business meaning and knowledge                                            | Data engineering pipelines                              | Database design                                           |
  | Audience             | Business users, BI developers, AI engineers, governance teams             | Data engineers                                          | Data architects, DBAs, application developers             |
  | Operates on          | Metadata, business concepts, metrics, relationships                       | Raw, cleansed, and curated datasets                     | Entities, attributes, and relationships                   |
  | Output               | Business metrics, knowledge graph, standardized definitions               | Bronze, Silver, Gold datasets                           | ERDs, schemas, tables, indexes                            |
  | Solves               | Consistent KPIs, semantic search, AI reasoning                            | Data quality, lineage, reproducibility                  | Efficient storage and data integrity                      |
  | Typical technologies | Semantic models, knowledge graphs, metadata catalogs, business glossaries | Lakehouse platforms, ETL/ELT frameworks                 | ER modeling tools, relational databases                   |
  | Example              | "Revenue", "Customer", "Harvest Productivity" have one agreed definition  | Bronze → Silver → Gold pipeline for sensor and ERP data | Customer, Order, Product tables with keys and constraints |
