---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Retention 101
parent: Statistics
permalink: /statistics/retention
nav_order: 104
---

# Retention 101
statistic
{: .badge .badge-pill .badge-primary }
retention
{: .badge .badge-pill .badge-secondary }
transaction
{: .badge .badge-pill .badge-info }

* Do not remove this line (it will not be displayed)
{:toc}

## Retention / Repeat Purchase
  This term used to answer this question:
  > How many of these customers came back and bought again?

  This term should be define more precise with:
  - who is being measured
  - when the clock starts
  - what counts as a repeat
  - whether we measure customers or orders

  - **Mental model**

  ```mermaid
  flowchart LR
  A[Customer] --> B[First Purchase]
  B --> C[Waiting Period]
  C --> D[Second Purchase]
  ```

## Retention Rate

  - **Example**
    - Imagine we have 100 customers at the beginning of a period. At the end of the period, 80 of them are still considered active. We retained: `80% of your customers`.

  - **Term**
    - "Active" could mean:
      - made another purchase
      - logged in
      - used the application
      - subscribed
      - opened an account
      - etc
    - Therefore, retention is not necessarily a purchase metric.
    - For active as a customer makes another purchase during a defined period, this could called as `cohort retention analysis`.

### Repeat Purchase Rate vs Retention Rate

  - **Term**
    - Repeat Purchase Rate
      - > Did the customer buy again?
      - Focused on a specific purchase window.
    - Retention Rate
      - > Are customers from this cohort still active after a certain period?
    - Repeat purchase is a specific behavioral event. Retention is a broader persistence concept.

## 30-day Repeat Purchase Rate

  - **Example**
    - 100 people buy something on the shop. wait in 30 days. if 25 of those 100 people buy something again, we called that:
      - **30-day repeat purchase rate = 25%**
    - Customer with first order at 1 jan, and has second order at 20 jan. This customer is qualifies as 30-day repeat purchase.

  - **Formula**

    $$
    \text{30-day Repeat Purchase Rate} = \frac{\text{Customers who purchase again within 30 days}}{\text{Customers who made the first purchase}} \times 100
    $$

  - The value of 30 days is flexible that could be change with any number days. Or we could set as overall repeat customer rate for calculate all repeate customer for all number days.

## Repurchase Rate

  - **Term**
    - `Repurchase rate` is often used almost synonymously with `repeat purchase rate`, but you should define it explicitly in your data model.
    - The important difference is eligibility. This eligibility is measured by a typical replacement cycle of product that customer used.

  - **Example**
    - Suppose a customer purchases a product with a typical replacement cycle of 90 days. If you measure repurchase after only 30 days, you may incorrectly conclude that customers aren't repurchasing.
    - > repurchase rate should consider the business/product purchase cycle

  - **Formula**

    $$
    \text{Repurchase Rate} = \frac{\text{Customers who purchased again}}{\text{Customers eligible to purchase again}} \times 100
    $$

## Repeat Customer Rate

  - **Term**
    - > What percentage of my customers have purchased more than once?
    - It doesn't necessarily care whether the second purchase happened within 30 days or any window time.

  - **Formula**

    $$
    \text{Repeat Customer Rate} = \frac{\text{Customers who purchased again}}{\text{Total Customers}} \times 100
    $$

## Comparison

  | Metric                          | Main question                                   | Time window?               | Typical denominator      |
  | ------------------------------- | ----------------------------------------------- | -------------------------- | ------------------------ |
  | **30-day Repeat Purchase Rate** | Did customers buy again within 30 days?         | Yes                        | First-purchase customers |
  | **Retention Rate**              | Are customers still active?                     | Usually                    | Starting cohort          |
  | **Repurchase Rate**             | Did eligible customers purchase again?          | Usually business-dependent | Eligible customers       |
  | **Repeat Customer Rate**        | Has the customer ever purchased more than once? | Not necessarily            | Total customers          |

  The terminology isn't universally standardized, so your metric definition document should explicitly state the numerator, denominator, and observation window.

## Cohort analysis
  
  | First Purchase Month | Month 0 | Month 1 | Month 2 | Month 3 |
  | -------------------- | ------: | ------: | ------: | ------: |
  | Jan                  |    100% |     45% |     30% |     20% |
  | Feb                  |    100% |     50% |     35% |     22% |
  | Mar                  |    100% |     47% |     31% |       — |
  | Apr                  |    100% |     52% |       — |       — |

  This answers: 
  > How well do customers from each acquisition cohort remain active?

## 30-day Repeat Purchase Rate vs Order Value

  - **Term**
    - > Does customer order value have a relationship with the probability that the customer purchases again within 30 days?

  - Data Structure
    - Data

      | Customer | First Order Date | First Order Value | Repeat Within 30d | Days to Next Order |
      | -------- | ---------------- | ----------------: | ----------------: | -----------------: |
      | A        | Jan 1            |               100 |                 1 |                  9 |
      | B        | Jan 2            |                50 |                 1 |                 18 |
      | C        | Jan 3            |               200 |                 0 |                  — |
      | D        | Jan 5            |               300 |                 0 |                 46 |
      | E        | Jan 8            |                40 |                 1 |                  7 |
      | F        | Jan 10           |                80 |                 0 |                 50 |
      | G        | Jan 12           |               150 |                 0 |                  — |
      | H        | Jan 15           |                70 |                 1 |                 10 |

    - Bucket Order Value

      | First Order Value | Customers | Repeat within 30d | 30-day Repeat Rate |
      | ----------------- | --------: | ----------------: | -----------------: |
      | $0–50             |       100 |                20 |                20% |
      | $51–100           |       150 |                45 |                30% |
      | $101–200          |       200 |                80 |                40% |
      | $201–500          |       120 |                60 |                50% |
      | $500+             |        50 |                30 |                60% |

    - **Plot 30-day repeat purchase rate vs first-order value from bucket order value data**.
    - This graph will tell us about:
      - > Customers with higher first-order value appear to have a higher probability of purchasing again within 30 days.

## Order Value vs Probability of Repeat

  - **Term**
    - A stronger approach is to model
      
      $$
      P(\text{Repeate_30d = 1}) = f(\text{First Order Value})
      $$

    - Given this customer's first order value, what is the probability they will repurchase within 30 days?

  - **Formula**
    - Using Logistic Regression
      
      $$
      logit(P(\text{Repeate_30d = 1})) = \beta_0 + \beta_1 \text{Order Value}
      $$

    - Or more advance

      $$
      logit(P(\text{Repeate_30d = 1})) = \beta_0 + \beta_1 \text{Order Value}+ \beta_2 \text{Discount}+ \beta_2 \text{Product Category} + \beta_3 \text{Product Category} + \beta_4 \text{Acquisition Channel} + \beta_5 \text{Customer Segment}
      $$