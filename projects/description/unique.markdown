---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Uniqueness
parent: Description Analytics
permalink: /description/uniqueness/
nav_order: 2
---

# Create Unique value in Data
descriptive analytics
{: .badge .badge-pill .badge-primary }

## Introduction
count and find uniqueness in each columns

## Dataset
### Load dataset
we use simple and common titanic dataset from seaborn library.

```python
df = sns.load_dataset("titanic")
```

|    |   survived |   pclass | sex    |   age |   sibsp |   parch |    fare | embarked   | class   | who   | adult_male   | deck   | embark_town   | alive   | alone   |
|---:|-----------:|---------:|:-------|------:|--------:|--------:|--------:|:-----------|:--------|:------|:-------------|:-------|:--------------|:--------|:--------|
|  0 |          0 |        3 | male   |    22 |       1 |       0 |  7.25   | S          | Third   | man   | True         | nan    | Southampton   | no      | False   |
|  1 |          1 |        1 | female |    38 |       1 |       0 | 71.2833 | C          | First   | woman | False        | C      | Cherbourg     | yes     | False   |
|  2 |          1 |        3 | female |    26 |       0 |       0 |  7.925  | S          | Third   | woman | False        | nan    | Southampton   | yes     | True    |
|  3 |          1 |        1 | female |    35 |       1 |       0 | 53.1    | S          | First   | woman | False        | C      | Southampton   | yes     | False   |
|  4 |          0 |        3 | male   |    35 |       0 |       0 |  8.05   | S          | Third   | man   | True         | nan    | Southampton   | no      | True    |

## The Code
By calling, `describe.unique` we can calculate and print all unique value in each columns with treshold value.

```python
describe.unique(df,r=0.1)
```

This function requires the following parameters:
- **main_data** (`dataframe`):      Data location and value  
- **r** (`float`):      ratio unique value

## The result

```
survived column has : 2 distinct values
[0 1]

pclass column has : 3 distinct values
[3 1 2]

sex column has : 2 distinct values
['male' 'female']

age column has : 89 distinct values
[22.   38.   26.   35.     nan 54.    2.   27.   14.    4.   58.   20.
 39.   55.   31.   34.   15.   28.    8.   19.   40.   66.   42.   21.
 18.    3.    7.   49.   29.   65.   28.5   5.   11.   45.   17.   32.
 16.   25.    0.83 30.   33.   23.   24.   46.   59.   71.   37.   47.
 14.5  70.5  32.5  12.    9.   36.5  51.   55.5  40.5  44.    1.   61.
 56.   50.   36.   45.5  20.5  62.   41.   52.   63.   23.5   0.92 43.
 60.   10.   64.   13.   48.    0.75 53.   57.   80.   70.   24.5   6.
  0.67 30.5   0.42 34.5  74.  ]

sibsp column has : 7 distinct values
[1 0 3 4 2 5 8]

parch column has : 7 distinct values
[0 1 2 5 3 4 6]

fare column has : 248 distinct values

embarked column has : 4 distinct values
['S' 'C' 'Q' nan]

class column has : 3 distinct values
['Third', 'First', 'Second']
Categories (3, object): ['Third', 'First', 'Second']

who column has : 3 distinct values
['man' 'woman' 'child']

adult_male column has : 2 distinct values
[ True False]

deck column has : 8 distinct values
[NaN, 'C', 'E', 'G', 'D', 'A', 'B', 'F']
Categories (7, object): ['C', 'E', 'G', 'D', 'A', 'B', 'F']

embark_town column has : 4 distinct values
['Southampton' 'Cherbourg' 'Queenstown' nan]

alive column has : 2 distinct values
['no' 'yes']

alone column has : 2 distinct values
[False  True]
```