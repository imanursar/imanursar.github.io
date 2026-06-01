---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Query Optimization
parent: Data Engineering
permalink: /data engineering/query-opt
nav_order: 104
---

#  Query Optimization
data engineering
{: .badge .badge-pill .badge-primary }
query
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

## Overview


## **Exploring**
### **Explore the root-cause using `EXPLAIN ANALYZE`**

```sql
EXPLAIN ANALYZE
SELECT * FROM users 
WHERE status = 'active' 
ORDER BY created_at DESC
LIMIT 100;
```

The output looked like this:

```sql
Limit   (cost=180234.89..180235.14 rows=100 width=524) 
        (actual time=47012.456..47012.789 rows=100 loops=1)
->  Sort    (cost=180234.89..185678.23 rows=2177336 width=524) 
            (actual time=47012.453..47012.612 rows=100 loops=1)
        Sort Key: created_at DESC
        Sort Method: top-N heapsort  Memory: 89kB
        ->  Seq Scan on users   (cost=0.00..125678.45 rows=2177336 width=524) 
                                (actual time=0.156..42341.234 rows=2180447 loops=1)
            Filter: ((status)::text = 'active'::text)
            Rows Removed by Filter: 28934
Planning Time: 2.341 ms
Execution Time: 47012.892 ms
```

- **Seq Scan**: PostgreSQL was reading the entire table. All 2.2 million rows. To find 100 results. `Seq Scan = Bad (Usually)`.
- **Sort = Maybe Bad**: If we see "Disk" in the sort? That's slow, PostgreSQL ran out of memory and is sorting on disk. Add an index that pre-sorts the data, or increase `work_mem`.

### **Identify the slow query**

```sql
SELECT query, calls, mean_exec_time, total_exec_time
FROM pg_stat_statements
ORDER BY mean_exec_time DESC
LIMIT 10;
```

### **Find duplicated rows in a table**

```sql
SELECT  Day, 
		Sales, 
        COUNT(*) 
FROM df2 
GROUP BY Day, Sales 
HAVING COUNT(*)>1
```


## **Optimize**
### **Index the importance columns `INDEX`**

```sql
CREATE INDEX idx_users_created_at ON users(created_at);
```

Every index:
- Takes disk space
- Slows down INSERT/UPDATE/DELETE
- Makes the query planner’s job harder

How to check usable index
```sql
SELECT schemaname, tablename, indexname, idx_scan
FROM pg_stat_user_indexes
WHERE idx_scan = 0 AND indexrelname NOT LIKE 'pg_toast%';

```

Index couldn't work with:
1. OR in WHERE Clause. Rewrite as UNION.
2. Function Calls on Indexed Column. we should indexing with function.
3. Indexes can’t help with leading wildcards. Use full-text search or pg_trgm extension.
4. NOT IN with Large Subquery. Use NOT EXISTS.

### **Index the importance combinational columns `INDEX`. Add an index that matches our WHERE clause.**

```sql
CREATE INDEX idx_users_status_created_at ON users(status, created_at DESC);
```

This index will help to get faster for 

```sql
SELECT * FROM users 
WHERE status = 'active' 
ORDER BY created_at DESC
LIMIT 100;
```

This will handle the `ORDER BY`, filter by `status`.

PostgreSQL reads indexes left to right. Thus for multiple index, it would be useless for last index. In example:

```sql
-- Index A
CREATE INDEX idx_a ON users(status, created_at);
-- Index B  
CREATE INDEX idx_b ON users(created_at, status);
```

For this query:

```sql
WHERE status = 'active' ORDER BY created_at
```

Index A: Find all status = 'active' rows (fast), they're already sorted by created_at (fast).
Index B: Find all rows sorted by created_at (all 2.2M rows), then filter by status (slow).

> **The rule: Match your WHERE clause first, then your ORDER BY.**


### **Put the most selective column first at `where` filter and index**

```sql
CREATE INDEX idx_users_email_status ON users(email, status);
```

This helps:

```sql
WHERE email = 'x' AND status = 'active'
```

This doesn’t:

```sql
WHERE status = 'active' AND email = 'x'
```

PostgreSQL can’t skip to the middle of an index.

### The value contained in IN in the SQL statement should not be too large
- Also note that `IN` and `NOT IN` must be used with caution, otherwise it will cause a full table scan.
- For consecutive values, you can use `BETWEEN` instead of using `IN`.
- If it is `IN`, then the subquery is executed first. So, `IN` is suitable for the case where the exterior is large and the interior is small; `Exists` is suitable for the case where the exterior is small and the interior is large.

### Avoid layers of nested sub-queries and replace them with CTEs
### Avoid including a HAVING clause in SELECT statements
### Avoid using OR in join conditions
### Avoid duplicate de-duping efforts
Avoid mixing UNION, DISTINCT, and window functions for deduplication purposes in one query. Keep in mind what is the granularity of the output from each CTE.
- **UNION** (instead of UNION ALL): when you need to combine data from several branches with the same structure while avoiding duplicates,
- **DISTINCT**: when you want to remove duplicate rows, and
- **window functions like ROW_NUMBER()**: when you want to keep rows with unique partition keys following certain criteria.
### Use EXISTS instead of DISTINCT when using table joins that involves tables having one-to-many relationships
### Use ‘regexp_like’ to replace multiple ‘LIKE’ clauses
### Use ‘regexp_extract’ to replace multiple ‘Case-when Like’
### Join very large tables at the last step if possible
by joining the large table at the end, you can filter and aggregate smaller tables first, reducing the data to be joined with the large table.


## **Technical**
### **Compute the cumulative**

```sql
SELECT 
    sales_month
    ,sales
    ,sum(sales) over (partition by date_part('year',sales_month)order by sales_month) as sales_ytd
FROM retail_sales
```

### **Z-score**

```sql
with 
sales_stats as(
	select avg(sales) as mean,
         stddev(sales) as sd
  from zscore
),
visitor_stats as(
		select avg(visitors) as mean,
            stddev(visitors) as sd
    from zscore
)

select dt,
    abs(sales - sales_stats.mean) / sales_stats.sd as z_score_sales,
    abs(visitors - visitor_stats.mean) / visitor_stats.sd as z_score_visitors
from sales_stats,
    visitor_stats,
    zscore;
```

### **Calculating Percent Change**

```sql
ROUND(IFNULL(100 * (row_count/LAG(row_count) OVER(ORDER BY row_count DESC) - 1), 0), 2) || '%' AS daily_percent_change
```

### **Calculate rolling time window**

```sql
SELECT 
    sales_month
    ,avg(sales) over (order by sales_month rows between 11 preceding and current row) as moving_avg
    ,count(sales) over (order by sales_month rows between 11 preceding and current row) as records_count
FROM retail_sales
```

### **Absolute difference and percent change**

```sql
SELECT 
    sales_month
    ,sales
    ,sales - lag(sales) over (partition by date_part('month',sales_month)order by sales_month) as absolute_diff
    ,(sales / lag(sales) over (partition by date_part('month',sales_month)order by sales_month)- 1) * 100 as pct_diff
FROM retail_sales
```


## params in Tools
### Postgres
- **work_mem**: help in sorting memory. `SET work_mem = '256MB'`
- **shared_buffers**: Should be ~25% of your total RAM
- **effective_cache_size**: Tell PostgreSQL how much RAM our OS uses for caching.
