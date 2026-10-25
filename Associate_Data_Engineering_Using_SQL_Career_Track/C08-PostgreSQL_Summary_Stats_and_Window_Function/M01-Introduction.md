# Introduction to Window Functions — Lesson Summary

## 1. Introduction

Welcome to the course! The instructor is Michel Semaan, who created the course together with Fernando Gonzalez Prada, owner of FGP Database and Analytics.

This course introduces SQL window functions and explains how they can simplify data analysis.

## 2. Why Use Window Functions?

Window functions simplify SQL queries that calculate running totals, retrieve previous or next row values, and rank records.

For example, calculating a running total of US gold medals since 2004 or retrieving previous Discus Throw champions would otherwise require complicated queries involving multiple self-joins and subqueries.

Window functions allow you to perform these operations more efficiently and with less code.

## 3. Course Outline

The course covers four main areas:

1. **Introduction to window functions:** Understand window functions, their common clauses, and basic functions.
2. **Fetching, ranking, and binning:** Retrieve values from other rows, rank records, and group values into categories.
3. **Aggregate window functions and frames:** Use functions such as `SUM()` as window functions and define which rows are included in calculations.
4. **Advanced techniques:** Explore additional SQL techniques and functions that work well with window functions.

## 4. Summer Olympics Dataset

Throughout the course, the examples use the Summer Olympics dataset, where each row represents an awarded medal.

The dataset contains columns such as:

- `year` — Year of the Olympic Games.
- `city` — Host city.
- `sport` — Sport category.
- `discipline` — Specific discipline.
- `event` — Competition event.
- `athlete` — Athlete's name.
- `country` — Represented country.
- `gender` — Athlete's gender.
- `medal` — Type of medal awarded.

## 5. What Are Window Functions?

A **window function** performs a calculation across a set of related rows while preserving each individual row in the result.

Unlike `GROUP BY`, which typically combines multiple rows into a single summary row per group, window functions return a calculated value for each row.

Window functions are useful for:

- Retrieving values from previous or following rows.
- Determining whether a champion has retained a title.
- Calculating growth over time.
- Ranking records.
- Calculating running totals.
- Calculating moving averages.

### Example: Aggregate Function vs. Window Function

Using `GROUP BY`:

```sql
SELECT
    country,
    COUNT(*) AS medal_count
FROM summer_medals
GROUP BY country;
```

This returns one row per country, showing its total number of medals.

Using a window function:

```sql
SELECT
    athlete,
    country,
    COUNT(*) OVER (
        PARTITION BY country
    ) AS country_medal_count
FROM summer_medals;
```

This displays each athlete's record while adding the total number of medal records associated with their country.

*Note: `summer_medals` is an illustrative table name. Use the actual table name in your database.*

## 6. Row Numbers

One of the simplest uses of a window function is assigning a sequential number to every row.

Row numbers let you identify records by their position in a query's result rather than by their actual values.

For example, you can assign row numbers to Olympic medal records.

### SQL Code: `ROW_NUMBER()`

```sql
SELECT
    athlete,
    country,
    year,
    ROW_NUMBER() OVER () AS row_num
FROM summer_medals;
```

**Explanation:**

- `ROW_NUMBER()` assigns a unique sequential number to each row.
- `OVER()` indicates that the function operates as a window function.
- `AS row_num` gives the generated column a name.

**Important:** Without an `ORDER BY` clause, the numbering order is not guaranteed. To assign row numbers consistently, specify the desired ordering.

For example:

```sql
SELECT
    athlete,
    country,
    year,
    ROW_NUMBER() OVER (
        ORDER BY year, athlete
    ) AS row_num
FROM summer_medals;
```

This numbers the records by year and then athlete name.

## 7. Anatomy of a Window Function

A window function generally follows this structure:

```sql
FUNCTION_NAME() OVER (
    PARTITION BY column_name
    ORDER BY column_name
    ROWS BETWEEN frame_start AND frame_end
)
```

The clauses inside `OVER()` are optional, depending on the function and the calculation you want.

| Component | Purpose |
|---|---|
| `FUNCTION_NAME()` | Specifies the operation, such as `ROW_NUMBER()`, `RANK()`, `SUM()`, or `AVG()`. |
| `OVER()` | Defines the window over which the function operates. |
| `PARTITION BY` | Divides rows into separate groups for independent calculations. |
| `ORDER BY` | Defines the order of rows within each window. |
| `ROWS` | Defines a frame using a specified number or range of physical rows. |
| `RANGE` | Defines a frame based on ordering values and their peers. |
| `PRECEDING` | Refers to rows or values before the current row, depending on the frame type. |
| `FOLLOWING` | Refers to rows or values after the current row, depending on the frame type. |
| `UNBOUNDED` | Extends the frame to the beginning or end of the partition. |

### Example: Number Athletes Within Each Country

```sql
SELECT
    athlete,
    country,
    year,
    ROW_NUMBER() OVER (
        PARTITION BY country
        ORDER BY year
    ) AS athlete_row_num
FROM summer_medals;
```

**How it works:**

- `PARTITION BY country` separates the records by country.
- `ORDER BY year` orders each country's records by year.
- `ROW_NUMBER()` assigns a sequential number within each country.

Each country starts its numbering at 1.

## 8. Key Takeaways

- Window functions perform calculations across related rows without collapsing the result into a single row per group.
- `ROW_NUMBER()` assigns a unique sequential number to each row.
- `OVER()` defines the window used by a window function.
- `PARTITION BY` creates separate groups for calculations.
- `ORDER BY` determines the order in which rows are processed.
- `ROWS`, `RANGE`, `PRECEDING`, `FOLLOWING`, and `UNBOUNDED` help define window frames for calculations such as running totals and moving averages.

## 9. Practice

Now that you've been introduced to window functions, practice using them in SQL exercises.

Start with `ROW_NUMBER()`, then progress to `PARTITION BY`, `ORDER BY`, ranking functions, and aggregate window functions.
