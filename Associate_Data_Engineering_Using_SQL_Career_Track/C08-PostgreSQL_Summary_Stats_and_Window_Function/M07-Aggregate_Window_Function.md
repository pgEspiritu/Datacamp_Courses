# SQL Window Functions: Aggregate Window Functions

## 1. Introduction to Aggregate Window Functions

In the previous chapter, we learned how to use window functions to:
- Fetch values using `LAG()`, `LEAD()`, `FIRST_VALUE()`, and `LAST_VALUE()`.
- Rank records using `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`.
- Divide records into groups using `NTILE()`.

In this chapter, we will explore how to use familiar SQL aggregate functions as **window functions**.

The aggregate functions covered include:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`

These functions can calculate summary statistics across an entire dataset or within a specified group. When used as window functions, they can also calculate values across rows while preserving individual records.

## 2. Understanding the Source Table

Suppose we want to examine the number of gold medals Brazil earned across five Olympic Games.

An example source query might look like this:

```sql
SELECT
    Year,
    COUNT(*) AS Medals
FROM Summer_Medals
WHERE
    Country = 'BRA'
    AND Medal = 'Gold'
    AND Year IN (1992, 1996, 2004, 2008, 2012)
GROUP BY Year
ORDER BY Year ASC;
```

This query counts Brazil's gold medals for each selected Olympic year.

**Illustrative source data:**

| Year | Medals |
|---|---:|
| 1992 | 13 |
| 1996 | 5 |
| 2004 | 18 |
| 2008 | 14 |
| 2012 | 14 |

This summarized dataset will be used to demonstrate aggregate window functions.

## 3. Using Standard Aggregate Functions

Before applying aggregate functions as window functions, let's review how they work in a regular SQL query.

Suppose the previous query is stored in a CTE named `Brazil_Medals`.

```sql
WITH Brazil_Medals AS (
    SELECT
        Year,
        COUNT(*) AS Medals
    FROM Summer_Medals
    WHERE
        Country = 'BRA'
        AND Medal = 'Gold'
        AND Year IN (1992, 1996, 2004, 2008, 2012)
    GROUP BY Year
)

SELECT
    MAX(Medals) AS Max_Medals,
    SUM(Medals) AS Total_Medals
FROM Brazil_Medals;
```

The result would be:

| Max_Medals | Total_Medals |
|---:|---:|
| 18 | 64 |

- `MAX(Medals)` returns the highest number of gold medals earned in a single year.
- `SUM(Medals)` calculates the total number of gold medals earned across all five Olympic Games.

These are standard aggregate functions. They summarize multiple rows into a single result.

**But what if we want to calculate the highest medal count so far or the cumulative total for every Olympic year?**

This is where aggregate window functions become useful.

## 4. Using MAX() as a Window Function

The `MAX()` function can be used as a window function to determine the highest value encountered so far in an ordered dataset.

### SQL Example

```sql
WITH Brazil_Medals AS (
    SELECT
        Year,
        COUNT(*) AS Medals
    FROM Summer_Medals
    WHERE
        Country = 'BRA'
        AND Medal = 'Gold'
        AND Year IN (1992, 1996, 2004, 2008, 2012)
    GROUP BY Year
)

SELECT
    Year,
    Medals,
    MAX(Medals) OVER (
        ORDER BY Year ASC
    ) AS Max_Medals
FROM Brazil_Medals
ORDER BY Year ASC;
```

### Explanation

- `MAX(Medals)` retrieves the highest medal count within the window.
- `OVER()` turns the aggregate function into a window function.
- `ORDER BY Year ASC` processes the Olympic Games chronologically.

Because the window is ordered by year, the maximum is calculated progressively as each new row is encountered.

### Expected Output

| Year | Medals | Max_Medals |
|---|---:|---:|
| 1992 | 13 | 13 |
| 1996 | 5 | 13 |
| 2004 | 18 | 18 |
| 2008 | 14 | 18 |
| 2012 | 14 | 18 |

### How Does MAX() Work Here?

1. **1992:** Brazil earned 13 medals. This is the first recorded value, so the maximum so far is 13.
2. **1996:** Brazil earned 5 medals. The previous maximum of 13 remains higher.
3. **2004:** Brazil earned 18 medals. This becomes the new maximum.
4. **2008:** Brazil earned 14 medals. The maximum remains 18.
5. **2012:** Brazil earned 14 medals again. The maximum remains 18.

The result shows the highest medal count recorded up to each Olympic year.

## 5. Using SUM() as a Window Function

The `SUM()` function can also be used as a window function to calculate a **cumulative sum**, also known as a running total.

A cumulative sum adds the current row's value to all preceding values in the ordered window.

### SQL Example

```sql
WITH Brazil_Medals AS (
    SELECT
        Year,
        COUNT(*) AS Medals
    FROM Summer_Medals
    WHERE
        Country = 'BRA'
        AND Medal = 'Gold'
        AND Year IN (1992, 1996, 2004, 2008, 2012)
    GROUP BY Year
)

SELECT
    Year,
    Medals,
    SUM(Medals) OVER (
        ORDER BY Year ASC
    ) AS Cumulative_Medals
FROM Brazil_Medals
ORDER BY Year ASC;
```

### Explanation

- `SUM(Medals)` calculates the total medals earned within the window.
- `OVER()` makes it a window function.
- `ORDER BY Year ASC` ensures that the cumulative sum follows chronological order.

### Expected Output

| Year | Medals | Cumulative_Medals |
|---|---:|---:|
| 1992 | 13 | 13 |
| 1996 | 5 | 18 |
| 2004 | 18 | 36 |
| 2008 | 14 | 50 |
| 2012 | 14 | 64 |

### How Does SUM() Work Here?

1. **1992:** 13 medals. Cumulative total = 13.
2. **1996:** 13 + 5 = 18.
3. **2004:** 13 + 5 + 18 = 36.
4. **2008:** 13 + 5 + 18 + 14 = 50.
5. **2012:** 13 + 5 + 18 + 14 + 14 = 64.

The cumulative sum increases as additional Olympic Games are included.

## 6. Partitioning with Aggregate Window Functions

Just like other window functions, aggregate window functions can also use `PARTITION BY`.

Suppose we want to calculate the cumulative gold medals earned by Brazil and Cuba separately.

Without partitioning, the cumulative sum includes the medal counts of both countries in one running total.

### A. Without PARTITION BY

```sql
SELECT
    Year,
    Country,
    Medals,
    SUM(Medals) OVER (
        ORDER BY Year ASC
    ) AS Cumulative_Medals
FROM Country_Medals
ORDER BY Year ASC;
```

In this example, the cumulative sum is calculated across the entire result set.

This means that the running total does not reset when the country changes.

### B. With PARTITION BY

```sql
SELECT
    Year,
    Country,
    Medals,
    SUM(Medals) OVER (
        PARTITION BY Country
        ORDER BY Year ASC
    ) AS Cumulative_Medals
FROM Country_Medals
ORDER BY Country ASC, Year ASC;
```

In this version:

- `PARTITION BY Country` divides the records into separate country groups.
- `ORDER BY Year ASC` calculates the cumulative sum chronologically within each country.
- The cumulative sum resets when a new country partition begins.

### Expected Output Concept

**Without partitioning:**

| Year | Country | Medals | Cumulative_Medals |
|---|---|---:|---:|
| 1992 | BRA | 13 | 13 |
| 1996 | BRA | 5 | 18 |
| 2004 | BRA | 18 | 36 |
| 1992 | CUB | 8 | 44 |
| 1996 | CUB | 10 | 54 |
| 2004 | CUB | 15 | 69 |

**With partitioning:**

| Year | Country | Medals | Cumulative_Medals |
|---|---|---:|---:|
| 1992 | BRA | 13 | 13 |
| 1996 | BRA | 5 | 18 |
| 2004 | BRA | 18 | 36 |
| 1992 | CUB | 8 | 8 |
| 1996 | CUB | 10 | 18 |
| 2004 | CUB | 15 | 33 |

*Illustrative values only.*

Notice the difference:

- Without `PARTITION BY`, the cumulative total continues across both countries.
- With `PARTITION BY Country`, each country's cumulative total is calculated independently.

## 7. Standard Aggregate Functions vs. Aggregate Window Functions

It is important to understand the difference between standard aggregation and window aggregation.

| Feature | Standard Aggregate | Aggregate Window Function |
|---|---|---|
| Example | `SUM(Medals)` | `SUM(Medals) OVER (...)` |
| Purpose | Calculates a summary | Calculates a value across a window |
| Individual rows | Usually collapsed when aggregated without grouping | Preserved |
| `GROUP BY` | Commonly used | Not required |
| `PARTITION BY` | Not applicable directly | Can divide the window into groups |

### Example: Standard Aggregate

```sql
SELECT
    Country,
    SUM(Medals) AS Total_Medals
FROM Country_Medals
GROUP BY Country;
```

This returns one row per country.

### Example: Aggregate Window Function

```sql
SELECT
    Year,
    Country,
    Medals,
    SUM(Medals) OVER (
        PARTITION BY Country
        ORDER BY Year ASC
    ) AS Cumulative_Medals
FROM Country_Medals;
```

This preserves every year-and-country record while adding the cumulative medal total.

## 8. Key Takeaways

- Aggregate functions such as `SUM()`, `MAX()`, `MIN()`, `AVG()`, and `COUNT()` can also be used as window functions.
- `MAX() OVER (ORDER BY ...)` can calculate the maximum value encountered so far.
- `SUM() OVER (ORDER BY ...)` can calculate a cumulative sum or running total.
- `PARTITION BY` allows aggregate calculations to be performed independently within groups.
- Window functions preserve individual rows, unlike standard aggregation that summarizes rows into groups.
- `ORDER BY` inside `OVER()` determines the sequence of the window calculation.

**Remember:** Aggregate window functions combine the summarizing power of aggregate functions with the row-preserving behavior of window functions. They are especially useful for running totals, cumulative averages, and tracking maximum or minimum values over time.
