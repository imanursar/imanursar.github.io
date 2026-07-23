---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Database Practice - Normalization
parent: Data Engineering
permalink: /data engineering/db_norm
nav_order: 80
---

#  Database Practice
data engineering
{: .badge .badge-pill .badge-primary }
database
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

## Database Normalization

  - **1NF - First Normal Form**
    - Eliminate repeating groups
    - Rules:
      - Each column must have atomic (unit) values.
      - No repeating groups or arrays.
    - Example:
      - there is no row with aggregate value.

      |ID |Name         | Phone    |
      |--:|------------:|:---------|
      | 1 | Alice       | 987      |
      | 2 | Alice       | 864      |
      | 3 | Bob         | 432      |
      | 4 | Charles     | 431      |
      | 5 | Charles     | 646      |

  - **2NF - Second Normal Form**
    - Remove partial dependencies
    - Rules:
      - Must be in 1NF.
      - Every non-key attribute must be fully functionally dependent on the whole primary key.
    - Example:

      |OrderID  | OrderDate       |
      |--------:|:----------------|
      | 101     | 2024-01-01      |
      | 102     | 2024-02-06      |
      | 103     | 2025-04-09      |
      | 120     | 2025-09-11      |
      | 110     | 2026-12-12      |

      |OrderID |ProductID| ProductName    | Price |
      |-------:|--------:|:---------------|:------|
      | 101    | 1       | Pen            | 10    |
      | 101    | 2       | Book           | 20    |
      | 102    | 1       | Pen            | 10    |

  - **3NF - Third Normal Form**
    - Remove transitive dependencies
    - Rules:
      - Must be in 2NF.
      - No transitive dependency. Non-key attributes should not depend on other non-key attributes.
    - Example:

      |EmpID |EmpName| DeptID |
      |-----:|------:|:-------|
      | 101  | Alice | 10     |
      | 102  | Bob   | 20     |
      | 103  | Charles| 10    |

      |DeptID  | DeptName        |
      |-------:|:----------------|
      | 10     | HR              |
      | 20     | IT              |

  - **BCNF - Boyce-Codd Normal**
    - Rules:
      - Must be in 3NF.
      - For every functional dependency X -> Y, X must be a super key.
    - Example:

      |DeptID  | Sub-Dept        |
      |-------:|:----------------|
      | 10     | Data            |
      | 10     | IT              |

      |Sub-Dept |name   |
      |--------:|------:|
      | Data    | Alice |
      | Data    | Bob   |
      | IT      | Charles|

  - **4NF - Forth Normal Form**
    - Remove multi-valued dependencies
    - Rules:
      - Must be in BCNF.
      - No no-trivial multi-valued dependencies.
    - Example:

      |EmpID |EmpName|
      |-----:|------:|
      | 101  | Alice |
      | 102  | Bob   |
      | 103  | Charles|

      |EmpID    | DeptName        |
      |--------:|:----------------|
      | 101     | HR              |
      | 102     | IT              |
      | 103     | IT              |

  - **5NF - Fifth Normal Form**
    - Remove join dependencies
    - Rules:
      - Must be in 4NF.
      - No join dependencies. Every fact must be represented in one table only.
    - Example:

      |EmpID |EmpName|
      |-----:|------:|
      | 101  | Alice |
      | 102  | Bob   |
      | 103  | Charles|

      |EmpName  | DeptName        |
      |--------:|:----------------|
      | Alice     | HR              |
      | Bob     | IT              |
      | Charles  | IT              |

      |DeptName| Sub-DeptName    |
      |-------:|:----------------|
      | HR     | GA              |
      | IT     | Infra           |
      | IT     | Software        |
