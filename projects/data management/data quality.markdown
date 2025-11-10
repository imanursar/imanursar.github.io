---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Data Quality
parent: Data Management BoK
permalink: /data management/data quality
nav_order: 101
---

#  Data Quality

data quality
{: .badge .badge-pill .badge-primary }
data government
{: .badge .badge-pill .badge-secondary }
data management
{: .badge .badge-pill .badge-info }

<img src="/assets/images/data/data_management/damas_01.webp" alt="drawing" width="500"/>

## Introduction
<p style='text-align: justify;'></p>

<p style='text-align: justify;'></p>

---

## Term and Concept of Data Quality management

- The term data quality:
    - The term data quality refers both to the characteristics associated with high quality data and to the processes used to measure or improve the quality of data. 
- The high quality mean:
    - Data is of high quality to the degree that it meets the expectations and needs of data consumers. Data quality is thus dependent on context and on the needs of the data consumer.
- **Data quality is about meeting expectations**. 
- **Metadata is a primary means of clarifying expectations**.
- **ISO 8000**, the international standard for data quality.
- **ISO 22745**, a standard for defining and exchanging Master Data.

---

## Goals of Data Quality Management

- Developing a governed approach to make data fit for purpose based on data consumers’ requirements
- Defining standards and specifications for data quality controls as part of the data lifecycle
- Defining and implementing processes to measure, monitor, and report on data quality levels
- Identifying and advocating for opportunities to improve the quality of data, through changes to processes and systems and engaging in activities that measurably improve the quality of data based on data consumer requirements

---

## Business drivers for Data Quality Management

- Increasing the value of organizational data and the opportunities use it
- Reducing risks and costs associated with poor quality data
- Improving organizational efficiency and productivity
- Protecting and enhancing the organization’s reputation
- The cost of getting data right the first time is cheaper than the costs from getting data wrong and fixing it later. 
- Maintaining high quality data throughout the data lifecycle is less risky than trying to improve quality in an existing process. 


### Data Quality Business Rule Types

- Describe how data should exist in order to be useful and usable within an organization. 
- These rules can be aligned with dimensions of quality and used to describe data quality requirements. 
- Common simple business rule types are:
    - **Definition conformance**: The same understanding of data definitions is implemented and used properly in processes across the organization.
    - **Value presence and record completeness**: Rules defining the conditions under which missing values are acceptable or unacceptable.
    - **Format compliance**: One or more patterns specify values assigned to a data element
    - **Value domain membership**: Specify that a data element’s assigned value is included in those enumerated in a defined data value domain
    - **Range conformance**: A data element assigned value must be within a defined numeric, lexicographic, or time range
    - **Mapping conformance**: Indicating that the value assigned to a data element must correspond to one selected from a value domain that maps to other equivalent corresponding value domain(s).
    - **Consistency rules**: Conditional assertions that refer to maintaining a relationship between two (or more) attributes based on the actual values of those attributes.
    - **Accuracy verification**: Compare a data value against a corresponding value in a system of record or other verified source to verify that the values match.
    - **Uniqueness verification**: Rules that specify which entities must have a unique representation and whether one and only one record exists for each represented real world object.
    - **Timeliness validation**: Rules that indicate the characteristics associated with expectations for accessibility and availability of data.

### Derivative rule types for aggregation
- Validate reasonableness of the number of records.
- Validate reasonableness of an average amount calculated from a set of numeric data.
- Validate the expected variance in the count of numeric data  over a specified timeframe

---

## Principles of Data Quality Management

- **Criticality**: should focus on the data most critical to the enterprise and its customers. 
- Should be **managed across the data lifecycle**, from creation or procurement through disposal.
- Should be on **preventing** data errors and conditions that reduce the usability
- **Root cause remediation**
- **Data Governance activities** must support the development of high quality data
- **Standards-driven**: All stakeholders in the data lifecycle have data quality requirements.
- **Objective measurement and transparency**: Data quality levels need to be measured objectively and consistently.
- **Embedded in business processes**: Business process owners are responsible for the quality of data produced through their processes.
- **Systematically enforced**: System owners must systematically enforce data quality requirements.
- **Connected to service levels**: Data quality reporting and issues management should be incorporated into Service Level Agreements (SLA).
- **Data Quality Management is a program** not a project, it will include both project and maintenance work, along with a commitment to communications and training and operational responsibilities.

---

## Data Quality Improvement Lifecycle

- Applying the techniques of quality improvement in the manufacture of physical products. 
- The goal is:  **To assess the relationship between inputs and outputs, in order to ensure that inputs meet the requirements of the process and that outputs conform to expectations**.
- Improvement comes through:
    - defined set of steps
    - measured against standards
    - identified root cause(s)
    - remediated
- Using Shew-hart / Deming cycle:
    - **PLAN** (assesses the scope, impact, and priority of known issues, and evaluates alternatives to address them. define cost and benefit, priority, formulated basic plan)
    - **DO** (to address the root causes of issues and plan for ongoing monitoring of data)
    - **CHECK** (involves actively monitoring the quality of data as measured against requirements)
    - **ACT** (for activities to address and resolve emerging data quality issues)