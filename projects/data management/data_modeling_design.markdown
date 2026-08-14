---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Data Modeling and Design
parent: Data Management BoK
permalink: /data management/data_model
nav_order: 105
---

# Data Modeling and Design

data modeling
{: .badge .badge-pill .badge-primary }
data government
{: .badge .badge-pill .badge-secondary }
data management
{: .badge .badge-pill .badge-info }

<img src="/assets/images/data/data_management/dm/dm_01.webp" alt="drawing" width="500"/>

* Do not remove this line (it will not be displayed)
{:toc}

## Introduction

Data modeling is the process of discovering, analyzing, and scoping data requirements, and then representing and communicating these data requirements in a precise form called the data model. 

Data models depict and enable an organization to understand its data assets.

The six most commonly used schemes are: Relational, Dimensional, ObjectOriented, Fact-Based, Time-Based, and NoSQL. Models of these schemes exist  at three levels of detail: conceptual, logical, and physical. Each model contains a set of components. Examples of components are entities, relationships, facts, keys, and attributes. Once a model is built, it needs to be reviewed and once approved, maintained.

<img src="/assets/images/data/data_management/dm/dm_01.webp" alt="drawing" />

## Business Drivers
Data models are critical to effective management of data. They:
- Provide a **common vocabulary** around data
- **Capture and document explicit knowledge** about an organization’s data and systems
- Serve as a **primary communications tool** during projects
- Provide the **starting point** for customization, integration, or even replacement of an application

## Goals and Principles
The goal of data modeling is to **confirm and document understanding** of different perspectives, which leads to applications that more closely align with current and future business requirements, and creates a foundation to successfully complete broad-scoped initiatives such as Master Data Management and data governance programs. Data models are an important form of Metadata.

Confirming and documenting understanding of different perspectives facilitates:
  - **Formalization**
    - A data model documents a concise definition of data structures and relationships. 
    - It enables assessment of how data is affected by implemented business rules, for current as-is states or desired target states. 
    - Formal definition imposes a disciplined structure to data that reduces the possibility of data anomalies occurring when accessing and persisting data. 
    - By illustrating the structures and relationships in the data, a data model makes data easier to consume.
  - **Scope definition**
    - A data model can help explain the boundaries for data context and implementation of purchased application packages, projects, initiatives, or existing systems.
  - **Knowledge retention/documentation** 
    - A data model can preserve corporate memory regarding a system or project by capturing knowledge in an explicit form. 
    - It serves as documentation for future projects to use as the as-is version.
    - Data models help us understand an organization or business area, an existing application, or the impact of modifying an existing data structure. 
    - The data model becomes a reusable map to help business professionals, project managers, analysts, modelers, and developers understand data structure within the environment. 
    - In much the same way as the mapmaker learned and documented a geographic landscape for others to use for navigation, the modeler enables others to understand an information landscape.

## Essential Concepts
Because data modeling itself is about the process of definition. It is important to understand the vocabulary that supports the practice.

### Data Modeling and Data Models
Data modeling is most frequently performed in the context of systems development and maintenance efforts, known as **the system development lifecycle (SDLC)**. Data modeling can also be performed for broad-scoped initiatives where the immediate end result is not a database but an understanding of organizational data.

**A model is a representation of something that exists or a pattern for something to be made**. A model can contain one or more diagrams. Model diagrams make use of standard symbols that allow one to understand content.

A data model contains a set of symbols with text labels that attempts visually to represent data requirements as communicated to the data modeler, for a specific set of data that can range in size from small, for a project, to large, for an organization. The model is a form of documentation for data requirements and data definitions resulting from the modeling process. 

### Types of Data that are Modeled
Four main types of data can be modeled:
- **Category information**: Data used to classify and assign types to things.
- **Resource information**: Basic profiles of resources needed conduct operational processes such as Product, Customer, Supplier, Facility, Organization, and Account. Resource entities are sometimes referred to as **Reference Data**.
- **Business event information**: Data created while operational processes are in progress. Event entities are sometimes referred to as **transactional business data**.
- **Detail transaction information**: Detailed transaction information is often produced through point-of-sale systems. This type of detailed information can be aggregated, used to derive other data, and analyzed for trends, similar to how the business information events are used. Type of data is usually referred to as **Big Data**.

These types refer to `data at rest`. Data in motion can also be modeled, for example, in schemes for systems, including protocols, and schemes for messaging and event-based systems.

## Data Model Components
Most data models contain the same basic building blocks: entities, relationships, attributes, and domains.

### Entity
Entity is a thing that exists separate from other things. Within data modeling, an entity is a thing about which an organization collects information. Entities are sometimes referred to as the nouns of an organization. An entity can be thought of as the answer to a fundamental question – who, what, when, where, why, or how – or to a combination of these questions.

Table below defines and gives examples of commonly used entity categories

| Category        | Definition                                                                                                                                                                                                                                                         | Examples                                                                                                 |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| **Who**         | Person or organization of interest. That is, _Who_ is important to the business? Often a 'who' is associated with a party generalization, or role such as Customer or Vendor. Persons or organizations can have multiple roles or be included in multiple parties. | Employee, Patient, Player, Suspect, Customer, Vendor, Student, Passenger, Competitor, Author             |
| **What**        | Product or service of interest to the enterprise. It often refers to what the organization makes or what service it provides. That is, _What_ is important to the business? Attributes for categories, types, etc. are very important here.                        | Product, Service, Raw Material, Finished Good, Course, Song, Photograph, Book                            |
| **When**        | Calendar or time interval of interest to the enterprise. That is, _When_ is the business in operation?                                                                                                                                                             | Time, Date, Month, Quarter, Year, Calendar, Semester, Fiscal Period, Minute, Departure Time              |
| **Where**       | Location of interest to the enterprise. Location can refer to actual places as well as electronic places. That is, _Where_ is business conducted?                                                                                                                  | Mailing Address, Distribution Point, Website URL, IP Address                                             |
| **Why**         | Event or transaction of interest to the enterprise. These events keep the business afloat. That is, _Why_ is the business in business?                                                                                                                             | Order, Return, Complaint, Withdrawal, Deposit, Compliment, Inquiry, Trade, Claim                         |
| **How**         | Documentation of the event of interest to the enterprise. Documents provide the evidence that the events occurred, such as a Purchase Order recording an Order event. That is, _How_ do we know that an event occurred?                                            | Invoice, Contract, Agreement, Account, Purchase Order, Speeding Ticket, Packing Slip, Trade Confirmation |
| **Measurement** | Counts, sums, etc. of the other categories (what, where) at or over points in time (when).                                                                                                                                                                         | Sales, Item Count, Payments, Balance                                                                     |

### Entity Aliases
In widespread use today is using the term *entity* for Employee and *entity instance* for Jane.

| Usage           | Entity   | Entity Type | Entity Instance |
| --------------- | -------- | ----------- | --------------- |
| Common Use      | Jane     | Employee    |                 |
| Recommended Use | Employee |             | Jane            |

Entity instances are the occurrences or values of a particular entity. 

In relational schemes the term *entity* is often used, in dimensional schemes the terms *dimension* and *fact table* are often used, in object-oriented schemes the terms class or object are often used, in timebased  schemes the terms *hub*, *satellite*, and *link* are often used, and in NoSQL schemes terms such as *document* or *node* are used.

An entity at the conceptual level can be called a *concept* or *term*, an entity at the logical level is called an *entity* (or a different term depending on the scheme), and at the physical level the terms vary based on database technology, the most common term being *table*.

### Graphic Representation of Entities
In data models, entities are generally depicted as rectangles.

### Definition of Entities
They are core Metadata. High quality definitions clarify the meaning of business vocabulary and provide rigor to the business rules governing entity relationships. 

High quality data definitions exhibit three essential characteristics:
- **Clarity**: The definition should be easy to read and grasp. Simple, well-written sentences without obscure acronyms or unexplained ambiguous terms such as sometimes or normally.
- **Accuracy**: The definition is a precise and correct description of the entity.
- **Completeness**: All of the parts of the definition are present. For example, in defining a code, examples of the code values are included. In defining an identifier, the scope of uniqueness in included in the definition.

### Relationship
A relationship is an association between entities. A relationship captures the high-level interactions between conceptual entities, the detailed interactions between logical entities, and the constraints between physical entities.

### Relationship Aliases
In relational schemes the term *relationship* is often used, dimensional schemes the term *navigation path* is often used, and in NoSQL schemes terms such as *edge* or *link* are used, for example. Relationship aliases can also vary based on level of detail.

### Graphic Representation of Relationships
Relationships are shown as lines on the data modeling diagram. A relationship is represented through foreign keys in a relational database and through alternative methods for NoSQL databases such as through edges or links.

### Relationship Cardinality
*Cardinality* captures how many of one entity (entity instances) participates in the relationship with how many of the other entity. 

Data rules are specified and enforced through cardinality. 

For cardinality, the choices are simple: zero, one, or many. Each side of a relationship can have any combination of zero, one, or many.

Specifying one or many allows us to capture how many of a particular instance participates in a given relationship.

### Arity of Relationships
The number of entities in a relationship is the `arity` of the relationship. The most common are unary, binary, and ternary relationships.

### Unary (Recursive) Relationship
A unary (also known as a recursive or self-referencing) involves only one entity. A one-to-many recursive relationship describes a hierarchy, whereas a many-to-many relationship describes a network or graph.

One can model this recursive relationship as either a **hierarchy** or **network**.

### Binary Relationship
An arity of two is also known as binary.

### Ternary Relationship
An arity of three, known as ternary, is a relationship that includes three entities. An example in fact-based modeling (object-role notation).

### Foreign Key
A foreign key is used in physical and sometimes logical relational data modeling schemes to represent a relationship. 

Foreign keys appear in the entity on the many side of the relationship, often called the child entity. E.g. Student and Course are parent entities and Registration is the child entity.

### Attribute
An attribute is a property that identifies, describes, or measures an entity. The physical correspondent of an attribute in an entity is a column, field, tag, or node in a table, view, document, graph, or file.

### Graphic Representation of Attributes
In data models, attributes are generally depicted as a list within the entity rectangle.

### Identifiers
An identifier (also called a key) is a set of one or more attributes that uniquely defines an instance of an entity. 

### Construction-type Keys
A simple key is one attribute that uniquely identifies an entity instance.

A **surrogate key** is a unique identifier for a table. A surrogate key is an integer whose meaning is unrelated to its face value. Surrogate
keys serve technical functions and should not be visible to end users of a database.

A **compound key** is a set of two or more attributes that together uniquely identify an entity instance. A composite key contains one compound key and at least one other simple or compound key or non-key attribute.

### Function-type Keys
A super key is any set of attributes that uniquely identify an entity
instance. 

A **candidate key** is a minimal set of one or more attributes (i.e., a simple or compound key) that identifies the entity instance to which it belongs. Minimal means that no subset of the candidate key uniquely identifies the entity instance. An entity may have multiple candidate keys.

A **business key** is one or more attributes that a business professional would use to retrieve a single entity instance. Business keys and surrogate keys are mutually exclusive.

A **primary key** is the candidate key that is chosen to be the unique
identifier for an entity. 

An **alternate key** is a candidate key that although unique, was not
chosen as the primary key.

Often the primary key is a surrogate key and thealternate keys are business keys.

### Dentifying vs. Non-Identifying Relationships
An independent entity is one where the primary key contains only
attributes that belong to that entity. A dependent entity is one where the primary key contains at least one attribute from another entity.

Independent entities on the data modeling diagram as rectangles and dependent entities as rectangles with rounded corners.

### Domain
a **domain** is the complete set of possible values that an attribute can be assigned. A domain provides a means of standardizing the characteristics of the attributes. 

One can restrict a domain with additional rules, called **constraints**. Rules can relate to format, logic, or both.

Domains can be defined in different ways:
- **Data Type**: Domains that specify the standard types of data one can have in an attribute assigned to that domain.
- **Data Format**: Domains that use patterns including templates and masks. e.g. character limitations (alphanumeric only, alphanumeric with certain special characters allowed, etc.) to define valid values.
- **List**: Domains that contain a finite set of values. 
- **Range**: Domains that allow all values of the same data type that are between one or more minimum and/or maximum values. Some ranges can be open-ended.
- **Rule-based**: Domains defined by the rules that values must comply with in order to be valid. These include rules comparing values to calculated values or other attribute values in a relation or set. For example, ItemPrice must be greater than ItemCost.

## Data Modeling Schemes
The six most common schemes used to represent data are: Relational, Dimensional, Object-Oriented, Fact-Based, Time-Based, and NoSQL.

| Scheme          | Sample Notations                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------- |
| Relational      | Information Engineering (IE), Integration Definition for Information Modeling (IDEF1X), Barker Notation, Chen |
| Dimensional     | Dimensional                                                                                             |
| Object-Oriented | Unified Modeling Language (UML)                                                                         |
| Fact-Based      | Object Role Modeling (ORM or ORM2), Fully Communication Oriented Modeling (FCO-IM)                        |
| Time-Based      | Data Vault, Anchor Modeling                                                                               |
| NoSQL           | Document, Column, Graph, Key-Value                                                                            |

- For the relational scheme, all three levels of models can be built for RDBMS, but only conceptual and logical models can be built for the other types of databases. 
- For the dimensional scheme, all three levels of models can be built for both RDBMS and MDBMS databases. 
- The object-oriented scheme works well for RDBMS and object databases.
- The time-based scheme is a physical data modeling technique primarily for data warehouses in a RDBMS environment. 
- The NoSQL scheme is heavily dependent on the underlying database structure (document, column, graph, or key-value), and is therefore a physical data modeling technique.

| Scheme              | Relational Database Management System (RDBMS) | Multidimensional Database Management System (MDBMS) | Object Databases | Document | Column | Graph  | Key-Value |
| ------------------- | --------------------------------------------- | --------------------------------------------------- | ---------------- | -------- | ------ | ------ | --------- |
| **Relational**      | CDM -> LDM -> PDM                             | CDM -> LDM                                          | CDM -> LDM       | CDM -> LDM| CDM -> LDM | CDM -> LDM | CDM -> LDM    |
| **Dimensional**     | CDM -> LDM -> PDM                             | CDM -> LDM -> PDM                                   |                  |          |        |        |           |
| **Object-Oriented** | CDM -> LDM -> PDM                             |                                                     | CDM -> LDM -> PDM|          |        |        |           |
| **Fact-Based**      | CDM -> LDM -> PDM                             | CDM -> LDM                                          | CDM -> LDM       | CDM -> LDM| CDM -> LDM | CDM -> LDM | CDM -> LDM    |
| **Time-Based**      | PDM                                           |                                                     |                  |          |        |        |           |
| **NoSQL**           |                                               |                                                     | PDM              | PDM      | PDM    | PDM    | PDM       |


### Relational
Dr. Edward Codd in 1970 found that data could most effectively be managed in terms of two-dimensional relations.

The design objectives for the relational model are to have an exact expression of business data and to have one fact in one place (the removal of redundancy). Relational modeling is ideal for the design of operational systems.

### Dimensional
Data is structured to optimize the query and analysis of large amounts of data. In contrast, operational systems that support transaction processing are optimized for fast processing of individual transactions.

Both the relational and dimensional conceptual data models can be based
on the same business process. The difference is in the meaning of the relationships, where on the relational model the relationship lines capture business rules, and on the dimensional model, they capture the navigation paths needed to answer business questions.

### Fact Tables
Within a dimensional scheme, the rows of a fact table correspond to particular measurements and are numeric, such as amounts, quantities, or counts. 

Metadata is critical to proper understanding and usage. Fact tables take up the most space in the database (90% is a reasonable rule of thumb), and tend to have large numbers of rows.

### Dimension Tables
Dimension tables represent the important objects of the business and contain mostly textual descriptions. 

Dimensions are typically highly denormalized and typically account for about 10% of the total data. Dimensions must have a unique identifier for each row. 

Dimensions also have attributes that change at different rates. Slowly changing dimensions (SCDs) manage changes based on the rate and type of change. 

- **Overwrite (Type 1)**: The new value overwrites the old value in place.
- **New Row (Type 2)**: The new values are written in a new row, and the old row is marked as not current.
- **New Column (Type 3)**: Multiple instances of a value are listed in columns on the same row, and a new value means writing the values in the series one spot down to make space at the front for the new value. The last value is discarded.

[Detail of SCD will discuss here](https://imanursar.github.io/data engineering/db_scds)

### Snowflaking
Snowflaking is the term given to normalizing the flat, single-table, dimensional structure in a star schema into the respective component hierarchical or network structures.

### Grain
The term *grain* stands for the meaning or description of a single row of data in a fact table; this is the most detail any row will have. Defining the grain of a fact table is one of the key steps in dimensional design.

### Conformed Dimensions
Conformed dimensions are built with the enterprise mindset. Where this allows these dimensions to be shared across dimensional models, due to containing consistent terminology and values. 

### Conformed Facts
Conformed facts use standardized definitions of terms across individual marts. Different business users may use the same term in different ways.

### Object-Oriented (UML)
The Unified Modeling Language (UML) is a graphical language for
modeling software. The UML class model specifies classes (entity types) and their relationship types.

- In entitiy relationship (ER), the closest equivalent to Operations would be Stored Procedures.
- Attribute types (e.g., Date, Minutes) are expressed in the implementable application code language and not in the physical database implementable terminology.

### Fact-Based Modeling (FBM)
Fact-based languages, a family of conceptual modeling languages, view the world in terms of objects, the facts that relate or characterize those objects, and each role that each object plays in each fact. 
- **Object Role Modeling (ORM or ORM2)**
  - ORM is a model-driven engineering approach that starts with typical examples of required information or queries presented in any external formulation familiar to users, and then verbalizes these examples at the conceptual level, in terms of simple facts expressed in a controlled natural language.
- **Fully Communication Oriented Modeling (FCO-IM)**
  - Is similar in notation and approach to ORM. it used number as  References to verbalizations of facts. 

### Time-Based
Time-based patterns are used when data values must be associated in chronological order and with specific time values.
- **Data Vault**
  - The Data Vault is a detail-oriented, time-based, and uniquely linked set of normalized tables that support one or more functional areas of business.
  - It is a hybrid approach, encompassing the best of breed between third normal form (3NF, to be discussed in Section 1.3.6) and star schema. 
  - Data Vaults are designed specifically to meet the needs of enterprise data warehouses. There are three types of entities: hubs, links, and satellites. 
  - Hubs, which represent the main concepts within a subject. 
  - Link, which relates two hubs.
  - Satellites that provide the descriptive information on the hub concepts and can support varying types of history.
- **Anchor Modeling**
  - Anchor Modeling is a technique suited for information that changes over time in both structure and content.
  - Anchor Modeling has four basic modeling concepts: anchors, attributes, ties, and knots. Anchors model entities and events, attributes model properties of anchors, ties model the relationships between anchors, and knots are used to model shared properties, such as states.

### NoSQL
It is less about how to query the database and more about how the data is stored. There are four main types of NoSQL databases: document, key-value, column-oriented, and graph.
- **Document**
  - Document databases frequently store the business subject in one structure called a document.
- **Key-value**
  - Key-value databases allow an application to store its data in only two columns (‘key’ and ‘value’), with the feature of storing both simple and complex information stored within the ‘value’ column.
- **Column-oriented**
  - RDBMSs work with a predefined structure and simple data types, such as amounts and dates, can work with more complex data types including unformatted text and imagery. In addition, column-oriented databases store each column in its own structure.
- **Graph**
  - A graph database is designed for data whose relations are well represented as a set of nodes with an undetermined number of connections between these nodes.

## Data Model Levels of Detail
Three-schema approach to database management. The three key components were:

- **Conceptual**: This embodies the `real world` view of the enterprise being modeled in the database. It represents the current ‘best model’ or ‘way of doing business’ for the enterprise.
- **External**: The various users of the database management system operate on subsets of the total enterprise model that are relevant to their particular needs. These subsets are represented as `external schemas`.
- **Internal**: The `machine view` of the data is described by the
internal schema. This schema describes the stored representation
of the enterprise’s information.

These three levels most commonly translate into the conceptual, logical, and physical levels of detail, respectively. Within projects, conceptual data modeling and logical data modeling are part of requirements planning and analysis activities, while physical data modeling is a design activity.

### Conceptual
A conceptual data model captures **the high-level data requirements** as a collection of related concepts. It **contains only the basic and critical business entities** within a given realm and function, with a description of each entity and the relationships between entities.

The relationship lines capture business rules on a relational data model.

### Logical
A logical data model is **a detailed representation of data requirements**, usually in support of a specific usage context, such as application requirements. Logical data models are still **independent of any technology or specific implementation constraints**. A logical data model often begins as an extension of a conceptual data model.

In a relational logical data model, the conceptual data model is extended
by adding attributes. Attributes are assigned to entities by applying the
technique of normalization. There is a very strong relationship between each attribute and the primary key of the entity in which it resides.

**A dimensional logical data model is in many cases a fully-attributed perspective of the dimensional conceptual data model**. Whereas the logical relational data model captures the business rules of a business process, the logical dimensional captures **the business questions to determine the health and performance of a business process**.

### Physical
A physical data model (PDM) represents a **detailed technical solution**, often using the logical data model as a starting point and then adapted to work within a set of hardware, software, and network tools.

**Physical data models are built for a particular technology**. Relational DBMSs, for example, should be designed with the specific capabilities of a database management system in mind.

Because the physical data model accommodates technology limitations, structures are often combined (denormalized) to improve retrieval performance.

### Canonical
A variant of a physical scheme is a Canonical Model, **used for data in motion between systems**. This model describes the structure of data being passed between systems **as packets or messages**. When sending data through web services, an Enterprise Service Bus (ESB), or through Enterprise Application Integration (EAI), the canonical model describes what data structure the sending service and any receiving services should use. These structures should be designed to be as generic as possible to enable re-use and simplify interface requirements. 

This structure may only be instantiated as a buffer or queue structure on an intermediary messaging system (middleware) to hold message contents temporarily.

### Views
A view is a virtual table. Views provide a **means to look at data from one or many tables that contain or reference the actual attributes**.

An instantiated (often called ‘materialized’) view runs at a predetermined time. Views are used to simplify queries, control data access, and rename columns, without the redundancy and loss of referential integrity due to denormalization.

### Partitioning
Partitioning refers to the process of splitting a table. It is performed to facilitate archiving and to improve retrieval performance.
- **Vertically split**: To reduce query sets, create subset tables that contain subsets of columns. 
  - For example, split a customer table in two based on whether the fields are mostly static or mostly volatile (to improve load / index performance), or based on whether the fields are commonly or uncommonly included in queries (to improve table scan performance).
- **Horizontally split**: To reduce query sets, create subset tables using the value of a column as the differentiator. 
  - For example, create regional customer tables that contain only customers in a specific region.

### Denormalization
Denormalization is **the deliberate transformation of normalized logical data model entities into physical tables with redundant or duplicate data structures**. denormalization intentionally puts one attribute in multiple places.

The first is to improve performance by:
- **Combining data** from multiple other tables in advance to avoid costly run-time joins.
- **Creating smaller, pre-filtered copies of data** to reduce costly run-time calculations and/or table scans of large tables.
- **Pre-calculating and storing costly data calculations** to avoid runtime system resource competition.

Denormalization can also be used to **enforce user security by segregating data into multiple views or copies** of tables according to access needs.

This process does introduce a risk of data errors due to duplication.

Denormalization is frequently chosen if structures such as views and partitions fall short in producing an efficient physical design. 

It is good practice to **implement data quality checks** to ensure that the copies of the attributes are correctly stored. In general, denormalize only to improve database query performance or to facilitate enforcement of user security.

The process does apply to other data models, one can denormalize in a document database, but it would be called something different – such
as *embedding*. 

In dimensional data modeling, denormalization is called *collapsing* or *combining*. If each dimension is collapsed into a single structure, the resulting data model is called a *Star Schema*. If the dimensions are not collapsed, the resulting data model is called a *Snowflake*.

### Normalization
Normalization is **the process of applying rules in order to organize business complexity into stable data structures**. The basic goal of normalization is to keep each attribute in only one place to eliminate redundancy and the inconsistencies that can result from redundancy.

Normalization rules sort attributes according to primary and foreign keys. Normalization rules sort into levels, with each level applying granularity and specificity in search of the correct primary and foreign keys. 

Each level comprises a separate normal form, and each successive level does not need to include previous levels. 

[Detail of Normalization will discuss here](https://imanursar.github.io/data%20engineering/db_norm)

The term normalized model usually means the data is in 3NF. 

### Abstraction
Abstraction is the removal of details in such a way as to broaden applicability to a wide class of situations while preserving the important properties and essential nature from concepts or subjects.

The modeler needs to weigh the cost of developing and maintaining an abstract structure versus the amount of rework required if the unabstracted structure needs to be modified in the future

Abstraction includes generalization and specialization. 
- Generalization groups the common attributes and relationships of entities into supertype entities.
- Specialization separates distinguishing attributes within an entity into subtype entities. This specialization is usually based on attribute
values within an entity instance.

Subtypes can also be created using roles or classification to separate instances of an entity into groups by function. The subtyping relationship implies that all of the properties from the
supertype are inherited by the subtype. 

Subtyping reduces redundancy on a data model. It also makes it easier to communicate similarities across what otherwise would appear to be distinct and separate entities.

## Plan for Data Modeling
A plan for data modeling contains tasks such as evaluating organizational requirements, creating standards, and determining data model storage.

### The deliverables of the data modeling process
1. **Diagram**: A data model contains one or more diagrams. The diagram is **the visual that captures the requirements in a precise form**. It depicts:
   - a level of detail (e.g., conceptual, logical, or physical)
   - a scheme (relational, dimensional, object-oriented, fact-based, time-based, or NoSQL)
   - a notation within that scheme (e.g., information engineering, unified modeling language, object-role modeling).
2. **Definitions**: Definitions for entities, attributes, and relationships are essential to maintaining the precision on a data model.
3. **Issues and outstanding questions**: Frequently the data modeling process raises issues and questions that may not be addressed during the data modeling phase. In addition, often the people or groups responsible for resolving these issues or answering these questions reside outside of the group building the data model. Therefore, often a document is delivered that contains the current set of issues and outstanding questions.
4. **Lineage**: For physical and sometimes logical data models, it is important to know the data lineage, that is, where the data comes from. Often lineage takes the form of a source/target mapping, where one can capture the source system attributes and how they populate the target system attributes. Lineage can also trace the data modeling components from conceptual to logical to physical within the same modeling effort. There are two reasons why lineage is important to capture during the data modeling. 
  - First, the data modeler will obtain a very strong understanding of the data requirements and therefore is in the best position to determine the source attributes. 
  - Second, determining the source attributes can be an effective tool to validate the accuracy of the model and the mapping (i.e., a reality check).

## Build the Data Model
Modelers study existing data models and databases, refer to published standards, and incorporate any data requirements. Modelers draft the model, and then return to business professionals and business analysts to clarify terms and business rules. They then update the model and ask more questions.

### Forward Engineering
Forward engineering is the process of building a new application beginning with the requirements. The CDM is completed first to understand the scope of the initiative and the key terminology within that scope. Then the LDM is completed to document the business solution, followed by the PDM to document the technical solution.

### Conceptual Data Modeling
Creating the CDM involves the following steps:
- **Select Scheme**: Decide whether the data model should be built following a relational, dimensional, fact-based, or NoSQL scheme. Refer to the earlier discussion on scheme and when to choose each scheme.
- **Select Notation**: Once the scheme is selected, choose the appropriate notation, such as information engineering or object role modeling. Choosing a notation depends on standards within an organization and the familiarity of users of a particular model with a particular notation.
- **Complete Initial CDM**: The initial CDM should capture the viewpoint of a user group. It should not complicate the process by trying to figure out how their viewpoint fits with other departments or with the organization as a whole.
  - Collect the highest-level concepts (nouns) that exist for the organization.
  - Then collect the activities (verbs) that connect these concepts. 
- **Incorporate Enterprise Terminology**: Once the data modeler has captured the users’ view in the boxes and lines, the data modeler next captures the enterprise perspective by ensuring consistency with enterprise terminology and rules. 
- **Obtain Sign-off**: After the initial model is complete, make sure the model is reviewed for data modeling best practices as well as its ability to meet the requirements.

### Logical Data Modeling
A logical data model (LDM) captures the detailed data requirements within the scope of a CDM.

- **Analyze Information Requirements**
  - To identify information requirements, one must first identify business information needs, in the context of one or more business processes. 
  - As their input, business processes require information products that are themselves the output from other business processes. The names of these information products often identify an essential business vocabulary that serves as the basis for data modeling. 
  - Requirements analysis includes the elicitation, organization, documentation, review, refinement, approval, and change control of business requirements. Some of these requirements identify business needs for data and information.
  - Logical data modeling is an important means of expressing business data requirements.
  - Written data requirement specification documents may be maintained using requirements management tools. The specifications gathered through the contents of any such documentation should carefully synchronize with the requirements captured with data models to facilitate impact analysis.
- **Analyze Existing Documentation**
  - It can often be a great jump-start to use pre-existing data artifacts, including already built data models and databases.
  - Make sure that any work done based on existing artifacts is validated by the SMEs for accuracy and currency. 
  - Creation of the LDM should take into account these data models and either use them, where applicable, or map them to the new enterprise data model. There could be useful data modeling patterns, such as a standard way of modeling the Party Role concept.
- **Add Associative Entities**
  - Associative entities are used to describe Many-to-Many (or Many-to-Many-to-Many, etc.) relationships. An associative entity takes the identifying attributes from the entities involved in the relationship, and puts them into a new entity that just describes the relationship between the entities. 
  - Associative entities may become nodes in graph databases. In dimensional modeling, associative entities usually become fact tables.
- **Add Attributes**
  - Add attributes to the conceptual entities. An attribute in a logical data model should be atomic. It should contain one and only one piece of data (fact) that cannot be divided into smaller pieces. 
- **Assign Domains**
  - Domains allow for consistency in format and value sets within and across projects. 
- **Assign Keys**
  - Attributes assigned to entities are either key or non-key attributes. A key attribute helps identify one unique entity instance from all others, either fully (by itself) or partially (in combination with other key elements).

### Physical Data Modeling
Logical data models require modifications and adaptations in order to have the resulting design perform well within storage applications. The term table will be used to refer to tables, files, and schemas; the term column to refer to columns, fields, and elements; and the term row to refer, to rows, records, or instances.

- **Resolve Logical Abstractions**
  - Logical abstraction entities (supertypes and subtypes) become separate objects in the physical database design using one of two methods.
    - Subtype absorption: The subtype entity attributes are included as nullable columns into a table representing the supertype entity.
    - Supertype partition: The supertype entity’s attributes are included in separate tables created for each subtype.
- **Add Attribute Details**
  - Add details to the physical model, such as the technical name of each table and column. 
  - Define the physical domain, physical data type, and length of each column or field. Add appropriate constraints (e.g., nullability and default values) for columns or fields, especially for NOT NULL constraints.
- **Add Reference Data Objects**
  - Small Reference Data value sets in the logical data model can be implemented in a physical model in three common ways:
    - **Create a matching separate code table**: Depending on the model, these can be unmanageably numerous.
    - **Create a master shared code table**: For models with a large number of code tables, this can collapse them into one table; however, this means that a change to one reference list will change the entire table. Take care to avoid code value collisions as well.
    - **Embed rules or valid codes into the appropriate object’s definition**: Create a constraint in the object definition code that embeds the rule or list. For code lists that are only used as reference for one other object, this can be a good solution.
- **Assign Surrogate Keys**
  - Assign unique key values that are not visible to the business and have no meaning or relationship with the data with which they are matched.
  -  if a surrogate key is assigned to be the primary key of a table, make sure there is an alternate key on the original primary key.
- **Denormalize for Performance**
  - Denormalizing or adding redundancy can improve performance so much that it outweighs the cost of the duplicate storage and synchronization processing. Dimensional structures are the main means of denormalization.
- **Index for Performance**
  - An index is an alternate path for accessing data in the database to optimize query (data retrieval) performance. 
  - Indexes can be unique or non-unique, clustered or non-clustered, partitioned or nonpartitioned, single column or multi-column, b-tree or bitmap or hashed.
  - Try to build indexes on large tables to support the most frequently run queries, using the most frequently referenced columns, particularly keys (primary, alternate, and foreign).
- **Partition	for	Performance**
  - The partitioning strategy of the overall data model (dimensional) especially when facts contain many optional dimensional keys (sparse). Ideally, partitioning on a date key is recommended; when this is not possible, a study is required based on profiled results and workload analysis to propose and refine the subsequent partitioning model.
-  **Create Views**
   - Views can be used to control access to certain data elements, or to embed common join conditions or filters to standardize common objects or queries.

### Reverse Engineering
Reverse engineering is the process of documenting an existing database.
- The PDM is completed first to understand the technical design of an existing system.
- LDM to document the business solution that the existing system meets,
- CDM to document the scope and key terminology within the existing system.

## Review the Data Models
Continuous improvement practices should be employed. Techniques such as time-to-value, support costs, and data model quality validators such as the Data Model Scorecard, can all be used to evaluate the model for correctness, completeness, and consistency.

## Maintain the Data Models
Updates to the data model need to be made when requirements change and frequently when business processes change. Within a specific project, often when one model level needs to change, a corresponding higher level of model needs to change. 

A good practice at the end of each development iteration is to reverse engineer the latest physical data model and make sure it is still consistent with its corresponding logical data model. 

## Data Modeling Tools
Data modeling tools are software that automate many of the tasks the data modeler performs. Entry-level data modeling tools provide basic drawing functionality including a data modeling pallet so that the user can easily create entities and relationships. These entry-level tools also support rubber banding, which is the automatic redrawing of relationship lines when entities are moved. More sophisticated data modeling tools support forward engineering from conceptual to logical to physical to database structures, allowing the generation of database data definition language (DDL). 

## Lineage Tools
A lineage tool is software that allows the capture and maintenance of the source structures for each attribute on the data model. These tools enable impact analysis; that is, one can use them to see if a change in one system or part of system has effects in another system.

## Data Profiling Tools
A data profiling tool can help explore the data content, validate it against existing Metadata, and identify Data Quality gaps/deficiencies, as well as deficiencies in existing data artifacts, such as logical and physical models, DDL, and model descriptions

## Metadata Repositories
A Metadata repository is a software tool that stores descriptive information about the data model, including the diagram and accompanying text such as definitions, along with Metadata imported from other tools and processes (software development and BPM tools, system catalogs, etc.). The repository itself should enable Metadata integration and exchange. Even more important than storing the Metadata is sharing the Metadata. 

## Data Model Patterns
Data model patterns are reusable modeling structures that can be applied to a wide class of situations. 
- **Elementary patterns** are the ‘nuts and bolts’ of data modeling. They include ways to resolve many-to-many relationships, and to construct self-referencing hierarchies. 
- **Assembly patterns** represent the building blocks that span the business and data modeler worlds. Business people can understand them – assets,
documents, people and organizations, and the like. Equally importantly,
they are often the subject of published data model patterns that can give
the modeler proven, robust, extensible, and implementable designs.
- **Integration patterns** provide the framework for linking the assembly
patterns in common ways.

## Industry Data Models
Industry data models are data models pre-built for an entire industry.
These models are often both broad in scope and very detailed. 

Any purchased data model will need to be customized to fit an organization, as it will have been developed from multiple other organizations’ needs. The level of customization required will depend on how close the model is to an organization’s needs, and how detailed the most important parts are. 

# Best Practices
## Best Practices in Naming Conventions
The ISO 11179 Metadata Registry, an international standard for representing Metadata in an organization, contains several sections related to data standards, including naming attributes and writing definitions.

Data modeling and database design standards serve as the guiding principles to effectively meet business data needs, conform to Enterprise and Data Architecture and ensure the quality of data.

Naming standards are particularly important for entities, tables, attributes, keys, views, and indexes. Names should be unique and as descriptive as possible.

**Logical** names should be **meaningful to business users**, using full words as much as possible and avoiding all but the most familiar abbreviations. **Physical** names must conform to the maximum length allowed by the DBMS, so use **abbreviations** where necessary. While **logical** names use **blank spaces** as separators between words, **physical** names typically use **underscores** as word separators.

Naming standards should minimize name changes across environments. Names should not reflect their specific environment, such as test, QA, or production. Class words, which are the last terms in attribute names such as Quantity, Name, and Code, can be used to distinguish attributes from entities and column names from table names. They can also show which attributes and columns are quantitative rather than qualitative, 

## Best Practices in Database Design
keep the following design principles in mind (PRISM):
- **Performance and ease of use**: Ensure quick and easy access to data by approved users in a usable and business-relevant form, maximizing the business value of both applications and data.
- **Reusability**: The database structure should ensure that, where appropriate, multiple applications can use the data and that the data can serve multiple purposes (e.g., business analysis, quality improvement, strategic planning, customer relationship management, and process improvement). Avoid coupling a database, data structure, or data object to a single application.
- **Integrity**: The data should always have a valid business meaning and value, regardless of context, and should always reflect a valid state of the business. Enforce data integrity constraints as close to the data as possible, and immediately detect and report violations of data integrity constraints.
- **Security**: True and accurate data should always be immediately available to authorized users, but only to authorized users. The privacy concerns of all stakeholders, including customers, business partners, and government regulators, must be met. Enforce data security, like data integrity, as close to the data as possible, and immediately detect and report security violations.
- **Maintainability**: Perform all data work at a cost that yields value by ensuring that the cost of creating, storing, maintaining, using, and disposing of data does not exceed its value to the organization. Ensure the fastest possible response to changes in business processes and new business requirements.

# Data Model Governance
## Data Model and Design Quality Management
- Data professionals must balance the data requirements of the information consumers and the application requirements of data producers. 
- Data professionals must also balance the short-term versus long-term
business interests.
- They must meet the long-term interests of all stakeholders by ensuring that an organization’s data resides in data structures that are secure, recoverable, sharable, and reusable, and that this data is as correct, timely, relevant, and usable as possible.
- Data models and database designs should be a reasonable balance between the short-term needs and the long-term needs of the enterprise.

## Develop Data Modeling and Design Standards
Data modeling and database design standards should include the following:
- A list and description of standard data modeling and database design deliverables
- A list of standard names, acceptable abbreviations, and abbreviation rules for uncommon words, that apply to all data model objects
- A list of standard naming formats for all data model objects, including attribute and column class words
- A list and description of standard methods for creating and maintaining these deliverables
- A list and description of data modeling and database design roles and responsibilities
- A list and description of all Metadata properties captured in data modeling and database design, including both business
- Metadata and technical Metadata. For example, guidelines may set the expectation that the data model captures lineage for each attribute.
- Metadata quality expectations and requirements
- Guidelines for how to use data modeling tools
- Guidelines for preparing for and leading design reviews
- Guidelines for versioning of data models
- Practices that are discouraged

## Review Data Model and Database Design Quality
The agenda for review meetings should include items for reviewing the starting model (if any), the changes made to the model and any other options that were considered and rejected, and how well the new model conforms to any modeling or architecture standards in place.

Participants must be able to discuss different viewpoints and reach group consensus without personal conflict, as all participants share the common goal of promoting the most practical, best performing and most usable design. 

## Manage Data Model Versioning and Integration
Note each change to a data model to preserve the lineage of changes over time. If a change affects the logical data model, such as a new or changed business data requirement, the data analyst or architect must review and approve the change to the model.

Each change should note:
- Why the project or situation required the change
- What and How the object(s) changed, including which tables had columns added, modified, or removed, etc.
- When the change was approved and when the change was made to the model (not necessarily when the change was implemented in a system)
- Who made the change
- Where the change was made (in which models)

# Data Modeling Metrics

The Data Model Scorecard, which provides 11 data model quality metrics: one for each of ten categories that make up the Scorecard and an overall score across all ten categories.

| #  | Category                                              | Total score | Model score | % | Comments |
| -- | ----------------------------------------------------- | ----------- | ----------- | - | -------- |
| 1  | How well does the model capture the requirements?     | 15          |             |   |          |
| 2  | How complete is the model?                            | 15          |             |   |          |
| 3  | How well does the model match its scheme?             | 10          |             |   |          |
| 4  | How structurally sound is the model?                  | 15          |             |   |          |
| 5  | How well does the model leverage generic structures?  | 10          |             |   |          |
| 6  | How well does the model follow naming standards?      | 5           |             |   |          |
| 7  | How well has the model been arranged for readability? | 5           |             |   |          |
| 8  | How good are the definitions?                         | 10          |             |   |          |
| 9  | How consistent is the model with the enterprise?      | 5           |             |   |          |
| 10 | How well does the metadata match the data?            | 10          |             |   |          |
|    | TOTAL SCORE                                           | 100         |             |   |          |


The model score column contains the reviewer’s assessment of how well a particular model met the scoring criteria, with a maximum score being the value that appears in the total score column. 

The comments column should document information that explains the score in more detail or captures the action items required to fix the model



































