---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: How to Calculate Distance
parent: Statistics
permalink: /statistics/distance
nav_order: 100
---

#  Distance Metrics - How to Calculate the Distance

geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
distance
{: .badge .badge-pill .badge-info }

<img src="/assets/images/geospatial/snippet/distance_01.png" alt="drawing" width="500"/>

## Introduction
<p style='text-align: justify;'>
Previously, we explored how to calculate the distance between multiple locations in a spatial context, focusing on geographical measurements such as <b>Euclidean distance or Haversine formula</b> for calculating the separation between two latitude-longitude points. <a href="https://imanursar.github.io/geospatial/distance">Read more here</a>. However, distance measurement extends far beyond just physical space.

In this section, we dive deeper into various mathematical distance metrics that are widely used in different domains, including text similarity, clustering, and machine learning. Each method serves a unique purpose, whether in <b>natural language processing (NLP), recommendation systems, image recognition, or statistical analysis</b>.
</p>

## Types of Distance Measures
In this guide, we’ll explore more various distance metrics that can be categorized based on their applications. Below, we explore several fundamental methods:

- **Spatial Distance Metrics (Used for Geographic and Multi-Dimensional Spaces)**
These methods are commonly applied to measure distances between locations or points in a multi-dimensional space, such as latitude-longitude coordinates or feature spaces in machine learning.

  - **Euclidean Distance** – The straight-line distance between two points, commonly used in spatial and machine learning models.
  
  - **Manhattan Distance** – Measures distance by summing the absolute differences of coordinates. It is useful in grid-based systems (like city blocks).

    The Manhattan distance, often called Taxicab distance or City Block distance, calculates the distance between real-valued vectors.
    Imagine vectors that describe objects on a uniform grid such as a chessboard.
    Manhattan distance then refers to the distance between two vectors if they could only move right angles. There is no diagonal movement involved in calculating the distance.

    It is a measure that is somewhat less intuitive than euclidean distance, especially when using in high-dimensional data.

    When your dataset has discrete and/or binary attributes, Manhattan seems to work quite well since it takes into account the paths that realistically could be taken within values of those attributes.
    Take Euclidean distance, for example, would create a straight line between two vectors when in reality this might not actually be possible.

  - **Chebyshev Distance** – Measures the greatest absolute difference along any coordinate dimension (useful in chess or board game movements).

    Chebyshev distance is defined as the greatest of difference between two vectors along any coordinate dimension. In other words, it is simply the maximum distance along one axis. Due to its nature, it is often referred to as Chessboard distance since the minimum number of moves needed by a king to go from one square to another is equal to Chebyshev distance.

    Chebyshev distance can be used to extract the minimum number of moves needed by aking to go from one square to another. Moreover, it can be a useful measure in games that allow unrestricted 8-way movement.
    
    In practice, Chebyshev distance is often used in warehouse logistics as it closely resembles the time an overhead crane takes to move an object.

  - **Minkowski Distance** – A generalized version of Manhattan and Euclidean distances, controlled by a parameter (p) to define its behavior.

    Minkowski distance is a bit more intricate measure than most. It is a metric used in Normed vector space (n-dimensional real space), which means that it can be used in a space where distances can be represented as a vector that has a length.

    This measure has three requirements:
      - **Zero Vector** — The zero vector has a length of zero whereas every other vector has a positive length. For example, if we travel from one place to another, then that distance is always positive. However, if we travel from one place to itself, then that distance is zero.
      - **Scalar Factor** — When you multiple the vector with a positive number its length is changed whilst keeping its direction. For example, if we go a certain distance in one direction and add the same distance, the direction does not change.
      - **Triangle Inequality** — The shortest distance between two points is a straight line.

    Common values of p are:
      - p=1 — Manhattan distance
      - p=2 — Euclidean distance
      - p=∞ — Chebyshev distance

  - **Mahalanobis Distance** – Accounts for correlations between variables and is useful for detecting outliers in multivariate data.

    The Mahalanobis distance is the distance between two points in a multivariate space. It’s often used to find outliers in statistical analyses that involve several variables.

- **Text Similarity Metrics (Used for NLP and String Matching)**
When comparing words, documents, or text sequences, traditional spatial distances aren’t sufficient. Instead, we rely on text-based distance metrics to quantify differences between sequences of characters or words.

  - **Cosine Similarity** – Measures the angle between two text vectors, often used for document similarity in NLP applications.
  
    Cosine similarity has often been used as a way to counteract Euclidean distance’s problem with high dimensionality. The cosine similarity is simply the cosine of the angle between two vectors. It also has the same inner product of the vectors if they were normalized to both have length one. 
    
    Disadvantage of cosine similarity is that the magnitude of vectors is not taken into account, merely their direction. this means that the differences in values are not fully taken into account. We use cosine similarity often when we have high-dimensional data and when the magnitude of the vectors is not of importance.

  - **Jaccard Similarity** – Computes similarity based on the ratio of shared elements to the total elements in two sets (used in keyword matching).

    The Jaccard index (or Intersection over Union) is a metric used to calculate the similarity and diversity of sample sets. It is the size of the intersection divided by the size of the union of the sample sets.

    In practice, it is the total number of similar entities between sets divided by the total number of entities. For example, if two sets have 1 entity in common and there are 5 different entities in total, then the Jaccard index would be 1/5 = 0.2.

    A major disadvantage of the Jaccard index is that it is highly influenced by the size of the data. Large datasets can have a big impact on the index as it could significantly increase the union whilst keeping the intersection similar.

    The Jaccard index is often used in applications where binary or binarized data are used. When you have a deep learning model predicting segments of an image, for instance, a car, the Jaccard index can then be used to calculate how accurate that predicted segment given true labels.

  - **Sorensen-Dice Coefficient** – Similar to Jaccard but gives more weight to common elements, making it useful for fuzzy matching.

    The Sørensen-Dice index is very similar to Jaccard index in that it measures the similarity and diversity of sample sets. Although they are calculated similarly the Sørensen-Dice index is a bit more intuitive because it can be seen as the percentage of overlap between two sets, which is a value between 0 and 1.

    Like the Jaccard index, they both overstate the importance of sets with little to no ground truth positive sets. As a result, it could dominate the average score taken over multiple sets. It weights each item inversely proportionally to the size of the relevant set rather than treating them equally.

  - **Levenshtein Distance (Edit Distance)** – Counts the minimum number of single-character edits (insertions, deletions, substitutions) required to transform one string into another (used in spell checkers and OCR systems).

    The Levenshtein distance is a metric to measure how apart are two sequences of words. In other words, it measures the minimum number of edits that you need to do to change a one-word sequence into the other. These edits can be insertions, deletions or substitutions.

    levenshtein_ratio_and_distance:
      - Calculates levenshtein distance between two strings.
      - If ratio_calc = True, the function computes the
      - levenshtein distance ratio of similarity between two strings
      - For all i and j, distance[i,j] will contain the Levenshtein distance between the first i characters of s and the first j characters of t

  - **Hamming Distance** – Measures the number of positions at which two strings of equal length differ (useful in error detection and DNA sequencing).

    Hamming distance is the number of values that are different between two vectors.It is typically used to compare two binary strings of equal length. It can also be used for strings to compare how similar they are to each other by calculating the number of characters that are different from each other. It is not advised to use this distance measure when the magnitude is an important measure.
    Use Hamming distance to measure the distance between categorical variables.


## Choosing the Right Distance Metric
Selecting the best distance metric depends on the type of data and the intended application:

- For Geospatial Analysis → Use Euclidean, Manhattan, or Haversine Distance
- For Clustering & Machine Learning → Use Minkowski or Mahalanobis Distance
- For Text Similarity (NLP) → Use Cosine, Jaccard, or Levenshtein Distance
- For Binary String Comparison → Use Hamming Distance
- For Statistical Analysis → Use Mahalanobis Distance


## The Code
By calling `statistic.distance`, we can measure distance in multiple list, matrixs with several methods. Some methods require additional parameter to get more precise value.

```python
statistic.distance(main_data_1,main_data_2,lon2=None,lat2=None,types='euclidean',case=None,p=None,ratio_calc=False,geometries='geojson')
```

This function requires the following parameters:
- **main_data_1** (`dataframe`):    Data location and value  
- **main_data_2** (`dataframe`):    Data location and value  
- **lon2** (`list or float`):       Data location and value  
- **lat2** (`list or float`):       Data location and value   
- **types** (`string`):             Type of method
- **case** (`string`):              subtype of method
- **p** (`int`):                    degree of method
- **ratio_calc** (`float`):         ratio of calculation
- **geometries** (`float`):         type of geometry in main data


in `types` parameter, we can calculate with there values:
- Geospatial Distance
  - euclidean
  - haversine
  - vincenty
  - osrm
  - osrm_path
- Spatial Distance Metrics
  - Euclidean
  - Manhattan
  - Chebyshev
  - Minkowski
  - Mahalanobis
- Non-spatial distance (e.g. Text Similarity)
  - Cosine
  - Jaccard
  - Sorensen
  - Levenshtein
  - Hamming


## The Code

Let say that we have the data like these one:

```python
X = [[0, 0, 0], [1, 1, 1]]
Y = [[1, 0, 0], [1, 1, 0]]
```
we can measure distance between these lists by several methods:
- **Cosine**
    ```python
    result = statistic.distance(main_data_1=X,main_data_2=Y,types='cosine')
    ```

    ```python
        [[0.     0.    ]
        [0.5774 0.8165]]
    ```

- **Humming**
    ```python
    result = statistic.distance(main_data_1=X[0],main_data_2=Y[1],types='humming', case ='dist')
    ```

    ```python
        2.0
    ```

    ```python
    result = statistic.distance(main_data_1=X[0],main_data_2=Y[0],types='humming', case ='cm')
    ```

    ```python
        0.3333
    ```

- **Manhattan**
    ```python
    result = statistic.distance(main_data_1=X[0],main_data_2=Y[1],types='humming', case ='dist')
    ```

    ```python
        [[1. 2.]
        [2. 1.]]
    ```

- **Chebyshev**
    ```python
    result = statistic.distance(main_data_1=X[0],main_data_2=Y[1],types='chebyshev')
    ```

    ```python
        1
    ```

- **Minkowski**
    ```python
    result = statistic.distance(main_data_1=X[0],main_data_2=Y[1],types='chebyshev')
    ```

    ```python
        1
    ```

- **Minkowski**
    ```python
    result = statistic.distance(main_data_1=X[0],main_data_2=Y[1],types='minkowski', p=1)
    ```

    ```python
        2.0
    ```

    ```python
    result = statistic.distance(main_data_1=X[0],main_data_2=Y[1],types='minkowski', p=2)
    ```

    ```python
        1.4142
    ```

    ```python
    result = statistic.distance(main_data_1=X[0],main_data_2=Y[1],types='minkowski', p=np.inf)
    ```

    ```python
        1.0
    ```

- **Jaccard**
    ```python
    result = statistic.distance(main_data_1=X,main_data_2=Y,types='jaccard')
    ```

    ```python
        0.5
    ```

- **Sorensendice**
    ```python
    result = statistic.distance(main_data_1=X,main_data_2=Y,types='sorensendice')
    ```

    ```python
        1.0
    ```

- **Levenshtein**
    ```python
    result = statistic.distance(main_data_1=X,main_data_2=Y,types='levenshtein')
    ```

    ```python
        'The strings are 2 edits away'
    ```

    ```python
    result = statistic.distance(main_data_1=X,main_data_2=Y,types='levenshtein', ratio_calc = True)
    ```

    ```python
        0.0
    ```

- **Mahalanobis**
    ```python
        X = [[0, 0, 0], [1, 1, 1], [10, 2, 4]]
        Y = [[1, 0, 0], [1, 1, 0],[3, 5, 7]]
    ```

    ```python
    result = statistic.distance(main_data_1=X,main_data_2=Y,types='mahalanobis')
    ```

|    |   mahalanobis distances |   p_value |   mahalanobis robust distances |   p_value_robust |
|---:|------------------------:|----------:|-------------------------------:|-----------------:|
|  0 |            -1.35108e+18 |         1 |                         1.75   |         0.185877 |
|  1 |            -3.3777e+17  |         1 |                         1.2704 |         0.259692 |
|  2 |            -3.65332e+19 |         1 |                       nan      |       nan        |


## Final Thoughts
Understanding different distance metrics is crucial for a variety of applications, from mapping geographical points to measuring textual similarity and analyzing statistical relationships. Whether you're working in data science, machine learning, or computational linguistics, knowing when and how to apply these methods can significantly improve accuracy and efficiency in problem-solving.