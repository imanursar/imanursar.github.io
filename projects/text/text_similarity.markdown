---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Text similarity
parent: Text Analysis
permalink: /text/similar
nav_order: 100
---

# Text similarity

Text
{: .badge .badge-pill .badge-primary }
Similarity
{: .badge .badge-pill .badge-secondary }
LLM
{: .badge .badge-pill .badge-info }


## Introduction
Text similarity is essential to data science, powering duplicate detection, content clustering, and search systems. The challenge is identifying when different text strings convey the same meaning.

Raw text often contains inconsistent capitalization, special characters, and formatting. Python’s re module provides an efficient way to normalize these variations.

Regular expressions identify and replace unwanted patterns, including symbols, whitespace, and formatting inconsistencies, creating cleaner text for downstream analysis.

## Dataset
### Load dataset
we use simple generated data as follow:

```python
df = pd.DataFrame([
    "iPhone® 14 Pro Max",
    "IPHONE 14 pro max",
    "Apple iPhone 14 Pro Max 256GB",
    "iPhone14ProMax",
    "i-Phone 14 Pro Max",
    "Samsung Galaxy S23 Ultra",
    "SAMSUNG Galaxy S23 Ultra 5G",
    "Galaxy S23 Ultra (512GB)",
    "Samsung S23 Ultra",
    "wireless headphones",
    "bluetooth earbuds",
    "Sony WH-1000XM4 Headphones",
    "WH-1000XM4 Wireless Headphones",
], columns=['product'])
```

before we use the data above, we could transform the text into well defined format such as: lower case, spacing, and remove non-words.

```python
df['cleaned_text'] = df.map(text.text_manipulation, types=['lower_case','non_word','spacing'])
```

This give as:
- Removing special characters and symbols
- Standardizing case and formatting
- Cleaning messy product names
- Preparing text for similarity analysis

Function above give us well defined format text like below:

|    | product                        | cleaned_text                   |
| -- | ------------------------------ | ------------------------------ |
| 0  | iPhone® 14 Pro Max             | iphone 14 pro max              |
| 1  | IPHONE 14 pro max              | iphone 14 pro max              |
| 2  | Apple iPhone 14 Pro Max 256GB  | apple iphone 14 pro max 256gb  |
| 3  | iPhone14ProMax                 | iphone14promax                 |
| 4  | i-Phone 14 Pro Max             | i phone 14 pro max             |
| 5  | Samsung Galaxy S23 Ultra       | samsung galaxy s23 ultra       |
| 6  | SAMSUNG Galaxy S23 Ultra 5G    | samsung galaxy s23 ultra 5g    |
| 7  | Galaxy S23 Ultra (512GB)       | galaxy s23 ultra 512gb         |
| 8  | Samsung S23 Ultra              | samsung s23 ultra              |
| 9  | wireless headphones            | wireless headphones            |
| 10 | bluetooth earbuds              | bluetooth earbuds              |
| 11 | Sony WH-1000XM4 Headphones     | sony wh 1000xm4 headphones     |
| 12 | WH-1000XM4 Wireless Headphones | wh 1000xm4 wireless headphones |

With our test data established, we can build a comprehensive preprocessing function to handle these variations.

## Main Function 

```python
similarity_text(main_data, col_name, types='cosine')
```

This function requires the following parameters:
- **main_data** (`dataframe`):  Data input
- **col_name** (`string`):      column name
- **types** (`string`):         type of text similarity that we want to use

## difflib: Python’s Built-in Sequence Matching
difflib is a Python built-in module that provides similarity ratios. It analyzes character sequences to calculate similarity scores between text strings.

```python
text.similarity_text(df[['cleaned_text']], col_name='cleaned_text', types='difflib')
```

| no  | cleaned_text                   | cleaned_text_b                 | score |
| --- | ------------------------------ | ------------------------------ | ----- |
| 0   | iphone 14 pro max              | iphone 14 pro max              | 1.00  |
| 1   | iphone 14 pro max              | iphone 14 pro max              | 1.00  |
| 2   | iphone 14 pro max              | apple iphone 14 pro max 256gb  | 0.74  |
| 3   | iphone 14 pro max              | iphone14promax                 | 0.90  |
| 4   | iphone 14 pro max              | i phone 14 pro max             | 0.97  |
|     | ...                            | ...                            | ...   |
| 164 | wh 1000xm4 wireless headphones | samsung s23 ultra              | 0.17  |
| 165 | wh 1000xm4 wireless headphones | wireless headphones            | 0.78  |
| 166 | wh 1000xm4 wireless headphones | bluetooth earbuds              | 0.26  |
| 167 | wh 1000xm4 wireless headphones | sony wh 1000xm4 headphones     | 0.75  |
| 168 | wh 1000xm4 wireless headphones | wh 1000xm4 wireless headphones | 1.00  |

The limitation for this module:
- Sensitivity to word order.
- Poor handling of extra content.

Use difflib when:
- Character-Level Similarity
- Learning text similarity concepts
- Working with small datasets (<1000 records)
- External dependencies not allowed
- Simple typo detection is sufficient

## RapidFuzz: High-Performance Fuzzy String Matching
RapidFuzz is a high-performance fuzzy string matching library with C++ optimization. It addresses word reordering and complex text variations that difflib cannot handle effectively.

```python
text.similarity_text(df[['cleaned_text']], col_name='cleaned_text', types='fuzz')
```

| no  | cleaned_text                   | cleaned_text_b                 | score |
| --- | ------------------------------ | ------------------------------ | ----- |
| 0   | iphone 14 pro max              | iphone 14 pro max              | 1.00  |
| 1   | iphone 14 pro max              | iphone 14 pro max              | 1.00  |
| 2   | iphone 14 pro max              | apple iphone 14 pro max 256gb  | 0.90  |
| 3   | iphone 14 pro max              | iphone14promax                 | 0.90  |
| 4   | iphone 14 pro max              | i phone 14 pro max             | 0.97  |
| ... | ...                            | ...                            | ...   |
| 164 | wh 1000xm4 wireless headphones | samsung s23 ultra              | 0.26  |
| 165 | wh 1000xm4 wireless headphones | wireless headphones            | 0.90  |
| 166 | wh 1000xm4 wireless headphones | bluetooth earbuds              | 0.39  |
| 167 | wh 1000xm4 wireless headphones | sony wh 1000xm4 headphones     | 0.85  |
| 168 | wh 1000xm4 wireless headphones | wh 1000xm4 wireless headphones | 1.00  |

The limitation for this module:
- It excels at text-level variations but cannot understand meaning. When products serve identical purposes using different terminology, we need semantic understanding rather than pattern matching.

Use RapidFuzz when:
- Production Fuzzy Matching
- Processing thousands of records
- Need fast approximate matching
- Handling abbreviations and variations
- Text-level similarity is sufficient

## Sentence Transformers: AI-Powered Semantic Similarity
Surface-level text matching misses semantic relationships. Sentence Transformers, a library built on transformer neural networks, can understand that “wireless headphones” and “bluetooth earbuds” serve identical purposes by analyzing meaning rather than just character patterns.

```python
text.similarity_text(df[['cleaned_text']], col_name='cleaned_text', types='transformers')
```

| no  | cleaned_text                   | cleaned_text_b                 | score  |
| --- | ------------------------------ | ------------------------------ | ------ |
| 0   | iphone 14 pro max              | iphone 14 pro max              | 1.0000 |
| 1   | iphone 14 pro max              | iphone 14 pro max              | 1.0000 |
| 2   | iphone 14 pro max              | apple iphone 14 pro max 256gb  | 0.8176 |
| 3   | iphone 14 pro max              | iphone14promax                 | 0.9140 |
| 4   | iphone 14 pro max              | i phone 14 pro max             | 0.8671 |
| ... | ...                            | ...                            | ...    |
| 164 | wh 1000xm4 wireless headphones | samsung s23 ultra              | 0.1320 |
| 165 | wh 1000xm4 wireless headphones | wireless headphones            | 0.7437 |
| 166 | wh 1000xm4 wireless headphones | bluetooth earbuds              | 0.4543 |
| 167 | wh 1000xm4 wireless headphones | sony wh 1000xm4 headphones     | 0.8790 |
| 168 | wh 1000xm4 wireless headphones | wh 1000xm4 wireless headphones | 1.0000 |

Sentence Transformers unlocks semantic understanding at computational cost. The decision depends on whether conceptual relationships provide sufficient business value to justify resource overhead.

Use Sentence Transformers when:
- Semantic Understanding
- Conceptual relationships matter
- “wireless headphones” should match “bluetooth earbuds”
- Building recommendation systems
- Multilingual content similarity
- Compute resources are available

## JF jaro winkler similarity

```python
text.similarity_text(df.head()[['cleaned_text']], col_name='cleaned_text', types='jf_winkler')
```

| no | cleaned_text                  | cleaned_text_b                | score  |
| -- | ----------------------------- | ----------------------------- | ------ |
| 1  | iphone 14 pro max             | iphone 14 pro max             | 1.0000 |
| 2  | iphone 14 pro max             | apple iphone 14 pro max 256gb | 0.7444 |
| 3  | iphone 14 pro max             | iphone14promax                | 0.9647 |
| 4  | iphone 14 pro max             | i phone 14 pro max            | 0.8775 |
| 5  | iphone 14 pro max             | iphone 14 pro max             | 1.0000 |
| 6  | iphone 14 pro max             | iphone 14 pro max             | 1.0000 |
| 7  | iphone 14 pro max             | apple iphone 14 pro max 256gb | 0.7444 |
| 8  | iphone 14 pro max             | iphone14promax                | 0.9647 |
| 9  | iphone 14 pro max             | i phone 14 pro max            | 0.8775 |
| 10 | apple iphone 14 pro max 256gb | iphone 14 pro max             | 0.7444 |
| 11 | apple iphone 14 pro max 256gb | iphone 14 pro max             | 0.7444 |
| 12 | apple iphone 14 pro max 256gb | apple iphone 14 pro max 256gb | 1.0000 |
| 13 | apple iphone 14 pro max 256gb | iphone14promax                | 0.6847 |
| 14 | apple iphone 14 pro max 256gb | i phone 14 pro max            | 0.7625 |
| 15 | iphone14promax                | iphone 14 pro max             | 0.9647 |
| 16 | iphone14promax                | iphone 14 pro max             | 0.9647 |
| 17 | iphone14promax                | apple iphone 14 pro max 256gb | 0.6847 |
| 18 | iphone14promax                | iphone14promax                | 1.0000 |
| 19 | iphone14promax                | i phone 14 pro max            | 0.9333 |
| 20 | i phone 14 pro max            | iphone 14 pro max             | 0.8775 |
| 21 | i phone 14 pro max            | iphone 14 pro max             | 0.8775 |
| 22 | i phone 14 pro max            | apple iphone 14 pro max 256gb | 0.7625 |
| 23 | i phone 14 pro max            | iphone14promax                | 0.9333 |
| 24 | i phone 14 pro max            | i phone 14 pro max            | 1.0000 |

## Final Thoughts
When facing complex challenges, start with the most basic solution first, identify where it fails through testing, then strategically upgrade the failing component.

Build complexity incrementally based on real limitations, not anticipated ones.



