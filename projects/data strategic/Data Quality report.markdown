---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Data Quality Profiling Report
parent: Data Strategic
permalink: /data strategic/data quality report
nav_order: 103
---

#  Data Quality Profiling Report

data government
{: .badge .badge-pill .badge-primary }
data cleansing
{: .badge .badge-pill .badge-secondary }

## **Informations**

- Dataset: xxx_data_services_xxxxxxxx_gdb
- Date: 26 Agustus 2030 
- Source: link 
- Discalimer: need more follow-up for other data quality issues. 

## **Executive Summary**

Our profiling analysis identified **3 key data quality issues** in the data services (xxxxxxxx version):

1. **Duplicate entities.**
2. **Unusual coordinate value.**
3. **Duplicate longitude and latitude for difference entities.**

These issues create significant risks, including: 
- Data accuracy and reliability concerns in the datasets we deliver to clients. 
- Credibility and client trust impact, as delivering incorrect POIs undermines confidence in our services. 
- Lack of trust in our data service. 
- Misaligned Recommendations and insights. 
- Relationship Strain, if clients blame us for not detecting or addressing quality issues early. 
- Lost upsell opportunities, where advanced services cannot be offered due to poor underlying data quality. 

Maintaining high-quality entities data is critical not only for client decision-making but also for protecting our reputation and ensuring the scalability of future value-added services. This also opens the opportunity for a discussion on implementing a proper data management system to manage entities data end-to-end, with a particular focus on strengthening data acquisition, data management, and data quality practices. 


## **Detailed Profiling Reports**

### **Duplicate Entities**

- **Findings** — Duplicate entities for the combination between name, address, source, taxonomy, longitude and latitude.
- **Total Affected** — ~ 17.274 from 2457944 row data (0.7%)
- **Root Causes**
  -     As there is currently no established process (still with a manual process) for removing duplicate results from entities searches. 
  -     The data using automated scraping potentially generates repeating value. Which aligns with the source of duplicate entities that come from (but are not limited to) Google Map and the Simas Kemenag Website. 
- **Impacts**
  -     This issue will affect the accuracy and reliability of the data that we provide to clients. Especially when they are selecting a specific region and taxonomy, the result will not be accurate due to the high number of entities that repeatedly appear. 
  -     Misaligned Recommendations will appear due to some regions and taxonomy has a higher count value due to duplicate entities. 
- **Recommendation / To-Do** — Implement automated ETL that cleanses these data before we release the final version. 
- **Evidences**
  - At several taxonomy. There are more than 1 entity with the same values. (at the count column).
  <img src="/assets/images/data/data_strategic/dq_report_01.webp" alt="drawing"/>

  - At some categories, with more than 1 entities appearing in the table 
  <img src="/assets/images/data/data_strategic/dq_report_02.webp" alt="drawing"/>

  - Heavy duplicate data at xxxxxxxx xxxxx-xxxxx in xxxxxxxxxx. It appears almost 61 times in our data.
  <img src="/assets/images/data/data_strategic/dq_report_03.webp" alt="drawing"/>


### **Unusual Coordinate Value**

- **Findings** — Entitites with peculiar value at longitude and latitude. 
- **Total Affected** — (not yet calculated).
- **Root Causes**
  - It is assumed that the data source populates the coordinates by generating sequential values, resulting in longitude and latitude points arranged in a linear pattern. Consequently, the entitites appear visually as straight lines aligned along either longitude or latitude.  
  - Currently, we find this behavior at the taxonomy labeled as Education;School;Kindergarden from the Website Kemendikbud. 
  - This data is probably false due to the location in a remote or unusual place for its taxonomy or label. (E.g. Kindergarten at a river or hill) with almost the same value with sequential values for longitude and latitude. 
- **Impacts**
  - This issue will be easier to identify visually (e.g. user) but it is quite hard to manage since it comes from the data sources that we have prior belief this data is true.
  - This issue will affect the accuracy and reliability of the data that we provide to clients. 
  - 
- **Recommendation / To-Do**
  - Create backup of affected data.
  - Identify more deeply for this pattern and mark the affected rows.
  - manually cleansing these rows.  
- **Evidences**
  - First finding.
  <img src="/assets/images/data/data_strategic/dq_report_04.webp" alt="drawing"/>

  - This data is probably false due to the location in a remote or unusual place for its taxonomy or label. (E.g. Kindergarten at river or hill)
  <img src="/assets/images/data/data_strategic/dq_report_05.webp" alt="drawing"/>

  <img src="/assets/images/data/data_strategic/dq_report_06.webp" alt="drawing"/>
  <img src="/assets/images/data/data_strategic/dq_report_07.webp" alt="drawing"/>
  <img src="/assets/images/data/data_strategic/dq_report_08.webp" alt="drawing"/>


### **Duplicate longitude and latitude for difference Entitites**

- **Findings** — Some Entitites have different names and addresses but share identical coordinate values.  
- **Total Affected** — In total almost 732472 rows data with same tag and coordinate. Or almost 30% data.   
- **Root Causes**
  - Latest findings show that this issue comes from data sources without coordinate value (e.g., Google Maps). Thus, the main problem comes from inaccurate geocoding processes, which return the same location for all input data. 
  
  E.g., we found that Tanjung Rendan has POI with taxonomy ["government_and_public","communal","religion","mosque",null] has the same coordinate value for more than 17,419 rows of data.
- **Impacts**
  - This data will have a huge impact, especially for affected taxonomy, due to it will be giving wrong information about the Entitites density and aggregation value. 
  - This issue will affect the accuracy and reliability of the data that we provide to clients. 
  - Misaligned Recommendations will appear due to some regions and taxonomy has a higher count value due to duplicate entities. 
- **Recommendation / To-Do**
  - Create backup of affected data 
  - Identify more deeply for this pattern and mark the affected rows.
  - Manually cleansing these rows. 
  - Implement automated ETL that cleanses these data 
- **Evidences**
  - <img src="/assets/images/data/data_strategic/dq_report_09.webp" alt="drawing"/>
  - <img src="/assets/images/data/data_strategic/dq_report_10.webp" alt="drawing"/>
  - Final same coordinate and same tags 
  <img src="/assets/images/data/data_strategic/dq_report_11.webp" alt="drawing"/>

  In this table clearly show that (e.g.) data with tag [government_and_public, communal, religion, mosque, ] has 17419 rows with same coordinate and in total almost 18082 rows have same value regardless of the tag. You can see the rest have the same issue.


