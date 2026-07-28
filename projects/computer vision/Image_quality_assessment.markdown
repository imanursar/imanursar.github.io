---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Image Data Quality Assessment
parent: Computer Vision
permalink: /computer vision/dq_assessment
nav_order: 103
---

#  Imagery Data Quality Assessment

data government
{: .badge .badge-pill .badge-primary }
data quality
{: .badge .badge-pill .badge-secondary }


## Executive Summary
  
  This document presents the assessment of raster and vector data used for GeoAI-based land and asset classification. The review covers four key data components—raster imagery, polygon boundaries, polygon label objects, and selected label categories—and provides strategic recommendations to improve data consistency, model performance, and classification accuracy. 

  Key recommendations are summarized as follows:
  1. Raster Imagery 
     - **Downscale** resolution from 0.03–0.05 m to 0.5–1 m to optimize processing time and computational cost while maintaining adequate object-level accuracy. 
     - **Standardize** spatial references to WGS 1984 Web Mercator (Auxiliary Sphere) across all datasets. This will resolve errors in the spatial process. 
     - **Account for shadow distortion** in orthophotos that may affect object size accuracy. 
     - **Remove the poor-quality data** from training and inference/prediction process that will lead to error in results. 

  2. Polygon Boundaries
     - **Ensure availability of both boundary types**: main building area and extended asset area (including buffer zones). 
     - **Validate spatial alignment** to correct systematic boundary shifts observed in some datasets. 

  3. Polygon Label Objects
     - **Standardize label naming conventions** and consolidate similar classes.
     - **Exclude polygons outside boundary areas** to optimize model learning. 
     - **Review questionable label assignments** and correct misclassified areas. 
     - **Acknowledge model perception limits** — models classify based on visible imagery, not inferred real-world structures. 

  4. Selected Label Objects 
     - **Select labels based on business requirements** and dataset statistics (e.g., area size and frequency). 
     - **Group final classes** into four key categories: `Street`, `Vegetation`, `Bareland`, and `Building`. 

  5. Change-Type Interpretation 
     - Analyze change patterns between major classes to identify **meaningful transformations** (e.g., land development, vegetation growth). 
     - Implement validation rules to minimize **false-positive detections**, especially between visually similar or occluded features. 
     - These recommendations collectively aim to enhance data consistency, model training efficiency, and overall accuracy of spatial AI-based change detection workflows. 

## The Data
  - Raster Image
  - Polygon Boundary
  - Polygon label objects (e.g. lapangan, bangunan, kebun, etc) 
  - Selected label objects (from all labels we select the few to check it changing. E.g. from kebun to bangunan.) 

## Raster Imagery 
### Resolution Assessment
  The raster imagery exhibits a very high spatial resolution of approximately 0.03–0.05 m. While this precision allows for detailed object recognition, it significantly increases processing time during both training and inference phases. 

  <img src="/assets/images/computer_vision/dq_assessment/dqa_01.webp" alt="drawing"/>

  **Recommendation**:
  - Downscale imagery to a resolution between 0.5 m and 1 m to balance accuracy and computational efficiency.

  | Trade-Off Analysis | Description                                                                                                      |
  | ------------------ | ---------------------------------------------------------------------------------------------------------------- |
  | Advantages         | \- Reduced training and inference time <br> \- optimized for objects ≥ 0.5–1 m.                    |
  | Disadvantages      | \- Loss of detail for objects smaller than 0.5 m <br> \- shape simplification for fine structures. |

### Orthophoto Quality and Shadows
  Orthophotos contain shadow artifacts cast by elevated objects (trees, buildings). These may not significantly affect model training but can impact object area estimation and shape precision. Aside from that, we found that some data has poor quality data that will affect the training and inference/prediction process.

  <img src="/assets/images/computer_vision/dq_assessment/dqa_02.webp" alt="drawing"/>
  <img src="/assets/images/computer_vision/dq_assessment/dqa_03.webp" alt="drawing"/>

  **Recommendation**:
  - Apply shadow correction or mask generation to improve geometric accuracy when object size precision is critical. Remove the poor-quality data from training and inference/prediction process, keep in mind that this poor-quality data will lead to error in result.

### Spatial Reference Consistency
  Raster images and polygon boundaries currently use differing spatial references. Misaligned coordinate systems can introduce positional errors during training and spatial operations. This also gives an issue to Cell size or resolution information. We found that almost all the data from 2024 have no information about Cell size. **This issue will make some spatial process (e.g. resample) return an error**.

  <img src="/assets/images/computer_vision/dq_assessment/dqa_04.webp" alt="drawing"/>
  <img src="/assets/images/computer_vision/dq_assessment/dqa_05.webp" alt="drawing"/>

  **Recommendation**:
  - Standardize all datasets to WGS 1984 Web Mercator (Auxiliary Sphere) for consistency with global GIS references.

## Polygon Boundaries
### Boundary Completeness
  Some datasets lack the dual-boundary structure (main building area and extended asset area). Both boundaries are essential for detecting changes within the core property and identifying encroachments in surrounding buffer zones.

  <img src="/assets/images/computer_vision/dq_assessment/dqa_06.webp" alt="drawing"/>
  <img src="/assets/images/computer_vision/dq_assessment/dqa_07.webp" alt="drawing"/>

  **Recommendation**:
  - Ensure each dataset includes both boundary types to enable comprehensive change detection and encroachment analysis. With only a single boundary (e.g. main building area) we only can determine and measure change areas without encroachment areas information.
  
### Boundary Alignment
  A subset of datasets exhibits systematic spatial shifts (consistent directional offsets). These positional discrepancies cause mismatched object relationships and reduce training reliability.

  <img src="/assets/images/computer_vision/dq_assessment/dqa_08.webp" alt="drawing"/>
  <img src="/assets/images/computer_vision/dq_assessment/dqa_09.webp" alt="drawing"/>
  <img src="/assets/images/computer_vision/dq_assessment/dqa_10.webp" alt="drawing"/>

  **Recommendation**:
  - Conduct geometric alignment checks and apply corrective shifts or transformations before model integration. Although it is easier to solve if the issue happens on single or small data (e.g. shifting manually).

## Polygon Label Objects
### Label Consistency
  Label data substantially aids preprocessing efficiency. However, inconsistencies in naming and categorization were observed. The following label variations were identified across three datasets:

  ```
  ['JALAN', 'SEMAK', 'LAHAN_TERBUKA', 'PERAIRAN', 'LAPANGAN', 'KEBUN', 'PEKARANGAN', 'BANGUNAN', 'LAPANGAN', 'RUMPUT', 'JALAN', 'BANGUNAN', 'PERAIRAN', 'TANAMAN_CAMPURAN', 'TANAH_KOSONG', 'Jalan', 'Sungai', 'Kebun_Campuran', 'Lapangan', 'Lahan_Terbuka', 'Rumput', 'Bangunan', 'Kolam', 'Pekarangan', 'Rumah', 'Drainase']
  ```

  **Recommendation**:
  - Normalize label capitalization and naming.
  - Group semantically similar classes (e.g., Semak, Rumput, Kebun) under a unified category such as Vegetation.

### Spatial Validity
  Several labeled polygons were found outside the designated main or asset boundary areas. These features do not contribute to relevant training regions and may bias model predictions.

  <img src="/assets/images/computer_vision/dq_assessment/dqa_11.webp" alt="drawing"/>
  <img src="/assets/images/computer_vision/dq_assessment/dqa_12.webp" alt="drawing"/>

  **Recommendation**:
  - Exclude polygons located outside extended asset areas prior to training and inference. This leads to any changes outside extended asset areas that will not be detected.

### Label Accuracy
  In some cases, questionable labeling was identified. For example, refinery zones labeled as “Pekarangan” are inconsistent with their visual context.

  <img src="/assets/images/computer_vision/dq_assessment/dqa_13.webp" alt="drawing"/>

  **Recommendation**:
  - Perform a quality control review to verify and correct misclassified areas based on imagery interpretation and standardized label definitions.

### Model Perception Consideration
  GeoAI models recognize visible patterns rather than inferred or logical structures. For example, a building partly obscured by tree canopy may be segmented as separate “Building” and “Vegetation” labels rather than a unified structure.

  In another words, we as humans will deductively extend that building label to make it a more suitable shape (e.g., rectangular), but the model only makes building labels for areas without tree canopy and makes another label (e.g., vegetation) for the canopy tree. There are some models that can extend their capability to make deductions about objects, but it requires more time and processing to do it.

  <img src="/assets/images/computer_vision/dq_assessment/dqa_14.webp" alt="drawing"/>

  **Recommendation**:
  - Define realistic model expectations and, where necessary, employ post-processing or geometric correction to improve feature completeness.

## Selected Label Objects
### Selection Framework
  Label selection should align with end-user objectives—primarily detecting transitions between land cover types (e.g., Kebun to Bangunan). Another way is to use existing data, examine it, select the frequent one, and group them into 5 or 6 big categories. By using 3 sample datasets (it is possible to use extended datasets), we can summarize which selected label objects are by this workflow Steps:
  1.	Aggregate all feature classes from each geodatabase.
  2.	Identify and extract the largest defined asset boundary polygon.
  3.	Select all label objects within this polygon.
  4.	Compute metrics: total count, area, and mean size per label.
  5.	Rank objects by descending area and occurrence frequency.

### Final Label Grouping
  Based on aggregated statistics, the following standardized label categories are recommended:

  | **Category** | **Included Labels (not limited to these lists)**        |
  | ------------ | ------------------------------------------------------- |
  | Street       | Jalan                                                   |
  | Vegetation   | Semak, Rumput, Kebun, Pekarangan                        |
  | Bare Land    | Lahan Terbuka, Lapangan, Tanah Kosong, Tanaman Campuran |
  | Building     | Bangunan, Rumah                                         |

  These categories simplify class management, enhance model performance, and align with most land use classification frameworks.

### Change-Type Interpretation and Potential False Positives
  In change detection workflows, transitions between major land-cover categories reveal significant spatial transformations. However, some transitions may result from **visual ambiguity, temporal differences, or imagery conditions rather than actual physical change**.

  The following matrix summarizes the expected and questionable change types:

  | From / To                     | Street | Vegetation                              | Bare Land                                           | Building                                 | Interpretation / Risk                                                                                        |
  | ----------------------------- | ------ | --------------------------------------- | --------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
  | Street → Vegetation           |        | Possible if unmaintained areas overgrow | Low probability                                     |                                          | Could indicate vegetation regrowth on unused roads or path misclassification                                 |
  | Street → Bare Land            |        |                                         | Possible (due to road removal or construction area) |                                          | Usually valid; check for seasonal imagery                                                                    |
  | Street → Building             |        |                                         |                                                     | Likely new construction over paved area  | High confidence                                                                                              |
  | Vegetation → Building         |        |                                         |                                                     | Valid development (e.g., new structures) | Common and meaningful change                                                                                 |
  | Building → Vegetation         |        | High                                    |                                                     |                                          | Potential **false positive**: tree canopy covering building, roof color change, or demolition site overgrown |
  | Building → Bare Land          |        |                                         | Possible demolition or cleared site                 |                                          | Can represent real demolition or misclassification                                                           |
  | Bare Land → Vegetation        |        | Valid (natural regrowth)                |                                                     |                                          | Often valid seasonal or post-construction recovery                                                           |
  | Bare Land → Building          |        |                                         |                                                     | Valid (construction activity)            | High confidence                                                                                              |
  | Vegetation ↔ Bare Land        |        | Common seasonal variation               |                                                     |                                          | Can indicate temporary clearance or growth cycle                                                             |
  | Street ↔ Bare Land / Building |        |                                         | Possible construction/redevelopment                 |                                          | Context-dependent, requires visual validation                                                                |

### Common Sources of False Positives

  | Scenario                                                         | Description                                                                        | Mitigation Strategy                                                                   |
  | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
  | Building → Vegetation                                            | Tree canopy or shadow covers building roof, model reclassifies area as vegetation. | Apply canopy mask or integrate multi-temporal data.                                   |
  | Vegetation → Bare Land                                           | Seasonal harvesting or temporary clearing misclassified as permanent change.       | Use temporal stacking to confirm persistence.                                         |
  | Bare Land → Building (false)                                     | Construction materials or ground textures resemble rooftops.                       | Integrate object-shape and context filtering (rectangular patterns, adjacency rules). |
  | Street → Building                                                | Parking lots or wide pavements interpreted as building rooftops.                   |                                                                                       | Parking lots or wide pavements interpreted as building rooftops. | Include spectral and texture features in model training. |
  |                                                                  |
  | Parking lots or wide pavements interpreted as building rooftops. |
  | Vegetation → Street                                              | Bare soil or dry vegetation resembling pavement.                                   | Enhance spectral normalization and contextual checks.                                 |



