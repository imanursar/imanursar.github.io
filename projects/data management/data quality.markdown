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

<img src="/assets/images/data/data_management/damas_03.webp" alt="drawing" width="500"/>

## Introduction
<p style='text-align: justify;'>
Data quality defines the credibility of every decision, analysis, and system that depends on information. It is not a cosmetic process or technical afterthought—it is a controlled discipline that determines whether data can be trusted, reused, and acted upon. Managing data quality begins with a shared understanding of its terms and concepts: accuracy, completeness, consistency, and timeliness are not ideals but measurable conditions. Quality management provides the structure to evaluate and correct data continuously, ensuring it remains aligned with business purpose and regulatory expectation.</p>

<p style='text-align: justify;'>
The goal of data quality management is to sustain confidence in data across its lifecycle. It links business drivers to operational principles, establishing a framework for assessment, improvement, and governance. The lifecycle is iterative: measure, analyze, improve, and monitor. Techniques and activities—profiling, validation, cleansing, and stewardship—exist to enforce these standards, not decorate them. Implementation succeeds only when governance embeds accountability into process and culture. Data quality is not achieved once; it is maintained deliberately, as part of how the organization works.
</p>

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

### Data Profiling

- Is a form of data analysis used to inspect data and assess quality.
- Data profiling uses statistical techniques to discover the true structure, content, and quality of a collection of data.
- Single, cross-column, multiple columns analysis.
- Can use profiling results to confirm known relationships and uncover hidden characteristics and patterns within and between data sets, including business rules, and validity constraints. 
- Results of data profiling can be used to identify opportunities to improve the quality of both data and Metadata.
- It enables organizations to identify potential problems. Solving problems requires other forms of analysis, including business process analysis, analysis of data lineage, and deeper data analysis that can help isolate root causes of problems.

### The steps to perform a full data profiling and analysis
- Define goals
- Understand data uses and risks
- Measure against rules
- Document and confirm findings with SMEs
- Use this information to prioritize remediation and improvement efforts


### Data Cleansing

- Scrubbing transforms data to make it conform to data standards and domain rules.
Cleansing includes detecting and correcting data errors to bring the quality of data to an acceptable level.
- Ideally, the need for data cleansing should decrease over time, as root causes of data issues are resolved. The need for data cleansing can be addressed by:
  - Implementing controls to prevent data entry errors
  - Correcting the data in the source system
  - Improving the business processes that create the data

### Data Enhancement

- Is the process of adding attributes to a data set to increase its quality and usability. Examples:
  - Time/Date stamps
  - Audit data
  - Reference vocabularies
  - Contextual information
  - Geographic information
  - Demographic information
  - Psychographic information
  - Valuation information

### Data Parsing, Formatting, Transformation and Standardization

- The process of analyzing data using pre-determined rules to define its content or value.
- Many data quality issues involve situations where variation in data values representing similar concepts introduces ambiguity.
  - When an invalid pattern is recognized, the application may attempt to transform the invalid value into one that meets the rules.
- A data quality tool parses data values that conform to any of those patterns, and even transforms them into a single, standardized form that will simplify the assessment, similarity analysis, and remediation processes.
- Readable does not always mean acceptable. Rules are created directly within a data integration stream, or rely on alternate technologies embedded in or accessible from within a tool.

---

## Tools for Data Quality 

- Data Profiling Tools
- Data Querying Tools
- Modeling and ETL Tools
- Data Quality Rule Templates
- Metadata Repositories

---

## Data Quality Critical Assessment

- Regulatory reporting
- Financial reporting
- Business policy
- Ongoing operations
- Business strategy, especially efforts at competitive
- Differentiation

## Assess readiness for data quality improvement

- What do stakeholders mean by ‘high quality data’?
- What is the impact of low quality data on business operations and strategy?
- How will higher quality data enable business strategy?
- What priorities drive the need for data quality improvement?
- What is the tolerance for poor quality data?
- What governance is in place to support data quality improvement?
- What additional governance structures will be needed?

## Assess the current state of data quality

- An understanding of business strategy and goals
- Interviews with stakeholders to identify pain points, risks, and business drivers
- Direct assessment of data, through profiling and other form of analysis
- Documentation of data dependencies in business processes
- Documentation of technical architecture and systems support for business processes

## Characteristics to assess for readiness to adopt data quality practices
- Management commitment to managing data as a strategic asset
- The organization’s current understanding of the quality of its data: they generally understand the obstacles and pain points that signify poor quality data.
- The actual state of the data: Finding an objective way to describe the condition of data that is causing pain points is the first step to improving the data.
- Risks associated with data creation, processing, or use: Identifying what can go wrong with data and the potential damage to an organization from poor quality data provides the basis for mitigating risks. 
- Cultural and technical readiness for scalable data quality monitoring: The quality of data can be negatively impacted by business and technical processes. 

---

## Factors for poor quality data

- Lack of understanding about the effects of poor quality
- Bad planning
- **Siloed** system design
- Inconsistent development processes
- Incomplete documentation
- A lack of standards, or a lack of governance. 
- Fail to define what makes data fit for purpose.

---

## Data Quality Dimensions

is a measurable feature or characteristic of data. it provides a vocabulary for defining data quality requirements.

- Characteristics that can be measured objectively
  - Completeness
  - Uniqueness
  - Validity
  - Timeliness
  - Accuracy
  - Consistency
- Subjective Interpretation
  - Usability (Accessibility)
  - Timing issues
  - Flexibility
  - Confidence
  - Value / validity
  - Interpret-ability (Ease of understanding)

---

## Framework for Data Quality strategy

- Understand and prioritize business needs
- Identify the data critical to meeting business needs
- Define business rules and data quality standards based on business requirements
- Assess data against expectations
- Share findings and get feedback from stakeholders
- Prioritize and manage issues
- Identify and prioritize opportunities for improvement
- Measure, monitor, and report on data quality
- Manage Metadata produced through data quality processes
- Integrate data quality controls into business and technical processes

---

## Data Quality Activities

### Define High Quality Data
- High quality data is fit for the purposes of data consumers. it is beneficial to understand business needs, define terms, identify organizational pain points, and start to build consensus about the drivers and priorities for data quality improvement.
- Ask a set of questions to understand current state and assess organizational readiness for data quality improvement.
- Getting a comprehensive picture of the current state of data quality.

### Define a Data Quality Strategy
- Data quality priorities must align with business strategy.
- DQ analysts will need to work closely with Data Stewards at all levels. They should also influence policy, including policy about business processes and systems development. 
- DQ work and a commitment to high quality data need to become embedded in organizational practices.

### Identify Critical Data and Business Rules
- Data Quality Management efforts should focus first on the most important data in the organization: data that, if it were of higher quality, would provide greater value to the organization and its customers.
- Need to identify business rules that describe or imply expectations about the quality characteristics of data. It may need to be reverse-engineered through analysis of existing business processes, workflows, regulations, policies, standards, system edits, software code, triggers and procedures, status code assignment and use, and plain old common sense.
- Most business rules are associated with how data is collected or created, but data quality measurement centers around whether data is fit for use. The two (data creation and data use) are related. People want to use data because of what it represents and why it was created. 
- It is possible to understand the process and rules by which data was created or collected. Measurements that describe whether data is fit for use should be developed in relation to known uses and measurable rules based on dimensions of data quality: completeness, conformity, validity, integrity, etc. that provide the basis for meaningful metrics.
- Defining data quality rules is challenging because most people are not used to thinking about data in terms of rules. It may be necessary to get at the rules indirectly, by asking stakeholders about the input and output.
- It also helps to ask about pain points, what happens when data is missing or incorrect, how they identify issues, how they recognize bad data.
- One of the best ways to get at rules is to share results of assessments. 

### Perform an Initial Data Quality Assessment
- The goal of an initial data quality assessment is to learn about the data in order to define an actionable plan for improvement.
- Looking at that data, querying it to understand data content and relationships, and comparing actual data to rules and expectations.
- It is usually best to start with a small, focused effort – a basic proof of concept.

### Identify and Prioritize Potential Improvements
- Identification may be accomplished by 
  - Full-scale data profiling of larger data sets to understand the breadth of existing issues. 
  - Interviewing stakeholders about the data issues that impact them and following up with analysis of the business impact of those issues.
- Prioritization requires a combination of data analysis and discussion with stakeholders.
- Profiling data is only the first step in analysis of data quality issues. It helps identify issues, but does not identify root causes, nor does it determine the impact of issues to business processes. 
- When planning large scale profiling, ensure that time is allocated to share results, prioritize problems, and determine which issues require in-depth analysis.

### Define Goals for Data Quality Improvement
- Remediation and improvement plans should account for quick hits – issues that can be addressed immediately at low cost – and longer-term strategic changes.
- The strategic focus of such plans should be to address root causes of issues and to put in place mechanisms to prevent issues in the first place.
- Be aware that many things can get in the way of improvement efforts:
  - system constraints
  - age of data
  - ongoing project work that uses the questionable data, 
  - overall complexity of the data landscape, 
  - cultural resistance to change. 
- To prevent the constraints from stalling the program, set specific, achievable goals based on consistent quantification of the business value of the improvements to data quality.
- Showing improvement will involve comparing initial measurements and improved results. 
- But the value comes with benefits of the improvement: fewer customer complaints, less time spent correcting errors, etc. 
- Measure these things to explain the value of the improvement work. No one cares about levels of field completeness unless there is a business impact. 
- Preventing issues generally costs less than correcting them sometimes orders of magnitude less.

### Develop and Deploy Data Quality Operations
- A DQ program should put in place:
  - A plan that allows the team to manage data quality rules and standards
  - Monitor data’s ongoing conformance with rules
  - Identify and manage data quality issues
  - Report on quality levels. 
- Data quality rules and standards are a critical form of Metadata.
- Two equally important reasons to implement operational data quality measurements:
  - To inform data consumers about levels of quality
  - To manage risk that change may be introduced through changes to business or technical processes
- Measurements intended to inform data consumers will focus on critical data elements and relationships that, if they are not sound, will directly impact business processes.
- Measurement results can be described at two levels: 
  - The detail related to the execution of individual rules
  - Overall results aggregated from the rules
- Each rule should have a standard, target, or threshold index for comparison.
  - **Valid_DQ = (tested rules - exceptions)/ tested rules**
  - **invalid_DQ = exceptions / tested rules**
- Measurements can be taken at three levels of granularity: 
  - The data element value, data instance or record, or the data set. 
- Decisions made during the issue management process should be tracked in an incident tracking system. 
- By documenting on tracking system, we could:
  - provide valuable insight about the causes and costs of data issues
  - a description of the issue and the root causes
  - options for remediation
  - the decision on how to resolve the issue
  - will collect performance data relating to issue resolution, work assignments, volume of issues, frequency of occurrence, as well as the time to respond, diagnose, plan a solution, and resolve issues.
  - knowledge about what has been changed, why it has been changed, and how it has been changed. 
- A data quality Service Level Agreement (SLA) specifies an organization’s expectations for response and remediation for data quality issues in each system. 
- This SLA will helps to manage an expectation that the operational procedures will provide a scheme for remediation of root causes within an agreed timeframe. 
- It is best to do this report in business terms to continually remind the organization of the direct effect that data has on customers.

### Develop Operational Procedures for Managing Data Issues
- Diagnosing issues; the objective is:
  - to review the symptoms of the data quality incident, it flow and isolate the location
  - trace the lineage of the data in question, evaluate whether there have been any environmental changes 
  - identify the problem and where it originated, evaluate whether or not there are any other process issues that contributed
  - pinpoint potential root causes of the problem, determine whether there are issues with external data
- Formulating options for remediation:
  - Addressing non-technical root causes
  - Modification of the systems to eliminate technical root causes
  - Developing controls to prevent the issue
  - Introducing additional inspection and monitoring
  - Directly correcting flawed data
  - Taking no action based on the cost and impact of correction versus the value of the data correction
- Resolving issues; the basic procedures are:
  - Assess the relative costs and merits of the alternatives
  - Recommend one of the planned alternatives
  - Provide a plan for developing and implementing the resolution
  - Implement the resolution

### To support effective tracking
- Standardize data quality issues and activities
- Provide an assignment process for data issues
- Manage issue escalation procedures
- Manage data quality resolution workflow


### Operational data quality control defined in a data quality SLA includes:
- Data elements covered by the agreement
- Business impacts associated with data flaws
- Data quality dimensions associated with each data element
- Expectations for quality for each data element for each of the identified dimensions in each application or system in the data value chain
- Methods for measuring against those expectations
- Acceptability threshold for each measurement
- Steward(s) to be notified in case the acceptability threshold is not met
- Timelines and deadlines for expected resolution or remediation of the issue
- Escalation strategy, and possible rewards and penalties

---

## Data Quality Techniques

### Preventive Actions
- The best way to create high quality data is to prevent poor quality data from entering an organization. Getting a comprehensive picture of the current state of data quality.

### Preventive Actions for Data Quality
- Establish data entry controls; Create data entry rules that prevent invalid or inaccurate data from entering a system.
- Train data producers; give a reason, impact and evaluation
- Define and enforce rules; Create a ‘data firewall,’ that can inspect the level of quality of data processed by an application
- Demand high quality data from data suppliers; assessment of how well their data will integrate and helps prevent the use of non-authoritative data.
- Implement Data Governance and Stewardship
- Institute formal change control; Ensure all changes to stored
- data are defined and tested before being implemented.

### Corrective Actions
- Data quality issues should be addressed systemically and at their root causes to minimize the costs and risks of corrective actions. ‘Solve the problem where it happens’ is the best practice in Data Quality Management
- Perform data correction in three general ways:
  - Automated correction: Automated correction techniques include rule-based standardization, normalization, and correction.
  - Manually-directed correction: Use automated tools but require manual review before committing the corrections to persistent storage.
  - Manual correction

### Quality Check and Audit Code Modules
Create shareable, linkable, and re-usable code modules that execute repeated data quality checks and audit processes that developers can get from a library

### Effective Data Quality Metrics
A critical component of managing data quality is developing metrics that inform data consumers about quality characteristics that are important to their uses of data.

### Statistical Process Control
- Statistical Process Control (SPC) is a method to manage processes by analyzing measurements of variation in process inputs, outputs, or steps.
- SPC is based on the assumption that when a process with consistent inputs is executed consistently, it will produce consistent outputs. 
- It uses measures of central tendency (how values cluster around a central value, such as a mean, median, or mode) and of variability around a central value (e.g., range, variance, standard deviation), to establish tolerances for variation within a process.
- Control chart
  - a time series graph that includes a central line for the average, and depicts calculated upper and lower control limits (variability around a central value).
  - In a stable process, measurement results outside the control limits indicate a special cause.
- SPC measures the predictability of process outcomes by identifying variation within a process. Processes have variation of two types:
  - Common Causes that are inherent in the process; a system is said to be in (statistical) control and a range of normal variation can be established
  - Special Causes that are unpredictable or intermittent. 

### Root Cause Analysis
A root cause of a problem is a factor that, if eliminated, would remove the problem itself. Root cause analysis is a process of understanding factors that contribute to problems and the ways they contribute.
Common techniques for root cause analysis include **Pareto analysis** (the 80/20 rule), **fishbone diagram analysis**, **track and trace**, **process analysis**, and **the Five Whys**

---

## Implementation Guidelines
- A hybrid approach works best – **top-down for sponsorship, consistency, and resources, but bottom-up to discover what is actually broken and to achieve incremental successes**.
- Improving data quality requires changes in how people think about and behave toward data. **Cultural change is challenging**. It requires planning, training, and reinforcement.

### Readiness Assessment / Risk Assessment
- How formal and well-supported a Data Quality program will be depends on how mature the organization is from a data management perspective. 
- Findings from a readiness assessment will help determine where to start and how quickly to proceed.

### Organization and Cultural Change
- The quality of data will not be improved through a collection of tools and concepts, but through a mindset that helps employees and stakeholders to act while always thinking of the quality of data and what the business and their customers need.
- The first step is promoting awareness about the role and importance of data to the organization. All employees must act responsibly and raise data quality issues, ask for good quality data as consumers, and provide quality information to others. Every person who touches the data can impact the quality of that data.

###  Accelerate the work of a Data Quality program by:
- Setting priorities
- Identifying and coordinating access to those who should be involved in various data quality-related decisions and activities
- Developing and maintaining standards for data quality
- Reporting relevant measurements of enterprise-wide data quality
- Providing guidance that facilitates staff involvement
- Establishing communications mechanisms for knowledge sharing
- Developing and applying data quality and compliance policies
- Monitoring and reporting on performance
- Sharing data quality inspection results to build awareness,
- Identify opportunities for improvements, and build consensus for improvements
- Resolving variations and conflicts; providing direction

### Training for implementation Data Quality should focus on:

- Common causes of data problems
- Relationships within the organization’s data ecosystem and why improving data quality requires an enterprise approach
- Consequences of poor quality data
- Necessity for ongoing improvement (why improvement is not a one-time thing)
- Becoming ‘data-lingual’, about to articulate the impact of data on organizational strategy and success, regulatory reporting, customer satisfaction

---

## Data Quality and Data Governance
Incorporating data quality efforts into the overall governance effort enables the Data Quality program team to work with a range of stakeholders and enablers:
Risk and security personnel who can help identify data-related organizational vulnerabilities.
Business process engineering and training staff who can help teams implement process improvements.
Business and operational data stewards, and data owners who can identify critical data, define standards and quality expectations, and prioritize remediation of data issues.

### Data Quality Policy
Data Quality efforts should be supported by and should support data governance policies.

### Manage Data Quality Rules
- Set clear expectations for data quality characteristics
- Provide requirements for system edits and controls that prevent data issues from being introduced
- Provide data quality requirements to vendors and other external parties
- Create the foundation for ongoing data quality measurement and reporting

### Metrics
Focus on measuring and reporting on quality. 
- **Measurability** - Expected results should be quantifiable within a discrete range.
- **Business relevance** - Every data quality metric should correlate with the influence of the data on key business expectations.
- **Acceptability** - Determine whether data meets business expectations based on specified acceptability thresholds. 
- **Accountability / Stewardship** - Metrics should be understood and approved by key stakeholders
- **Controllability** -  if the metric is out of range, it should trigger action to improve the data. If there is no way to respond, then the metric is probably not useful.
- **Trending** - Metrics enable an organization to measure data quality improvement over time.

### High-level categories of data quality metrics include:
- **Return on Investment**; Statements on cost of improvement efforts vs. the benefits of improved data quality.
- **Levels of quality**; Measurements of the number and percentage of errors or requirement violations within a data set or across data sets
- **Data Quality trends**; Quality improvement over time (i.e., a trend) against thresholds and targets, or quality incidents per period
- **Data issue management metrics**: 
  - Counts of issues by dimensions of data quality 
  - Issues per business function and their statuses (resolved, outstanding, escalated)
  - Issue by priority and severity
  - Time to resolve issues
- **Conformance to service levels**: Organizational units involved and responsible staff, project interventions for data quality assessments, overall process conformance.
- **Data Quality plan rollout**: As-is and roadmap for expansion

###  Determine ROI of fixes based on:
- The criticality (importance ranking) of the data affected
- Amount of data affected
- The age of the data
- Number and type of business processes impacted by the issue
- Number of customers, clients, vendors, or employees impacted by the issue
- Risks associated with the issue
- Costs of remediating root causes
- Costs of potential work-arounds

### Manage Metadata for Data Quality
- Documented consistently: Establish standards, formats and templates for documenting rules.
- Defined in terms of Data Quality dimensions: Dimensions of quality help people understand what is being measured.
- Tied to business impact: Standards and rules should be connected directly to their impact on organizational success.
- Backed by data analysis: Rules should be tested against actual data and analysis result.
- Confirmed by SMEs: to confirm or explain the results of data analysis.
- Accessible to all data consumers: and could to ask questions about and provide feedback on rules.

### Reporting should focus around:
- Data quality scorecard; which provides a high-level view of the scores associated with various metrics, reported to different levels of the organization within established thresholds.
- Data quality trends
- SLA Metrics
- Data quality issue management
- Conformance of the Data Quality team to governance policies
- Conformance of IT and business teams to Data Quality policies
- Positive effects of improvement projects

### Most Data Quality program implementations need to plan for:
- Metrics on the value of data and the cost of poor quality data: to raise organizational awareness of the need for Data Quality Management, provide the basis for funding improvements and changing the behavior.
- Operating model for IT/Business interactions: Business people know what the important data is, and what it means. 
- Changes in how projects are executed: Project oversight must ensure project funding includes steps related to data quality
- Changes to business processes: Improving data quality depends on improving the processes by which data is produced.
- Funding for remediation and improvement projects: Some organizations do not plan for remediating data, even when they are aware of data quality issues. Data will not fix itself.
- Funding for Data Quality Operations