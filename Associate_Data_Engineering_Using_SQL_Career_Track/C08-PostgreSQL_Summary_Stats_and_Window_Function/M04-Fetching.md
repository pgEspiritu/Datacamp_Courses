# SQL Window Functions — Fetching Values

## 1. Introduction to Fetching Functions

In Chapter 1, you learned the fundamentals of window functions, including `ROW_NUMBER()`, `ORDER BY`, and `PARTITION BY`.

In this chapter, you will explore practical applications of window functions, particularly how to fetch values from different rows and display them alongside the current row.

Fetching functions allow you to retrieve values from other positions within a table or partition without using complex self-joins.

## 2. The Four Fetching Functions

There are four commonly used fetching functions:

| Function | Purpose | Type |
|---|---|---|
| `LAG()` | Retrieves a value from a previous row. | Relative |
| `LEAD()` | Retrieves a value from a following row. | Relative |
| `FIRST_VALUE()` | Retrieves the first value in a window or partition. | Absolute |
| `LAST_VALUE()` | Retrieves the last value in a window or partition. | Absolute |

### Relative vs. Absolute Fetching

**Relative fetching functions**

- `LAG()` — Looks backward from the current row.
- `LEAD()` — Looks forward from the current row.

Their results depend on the position of the current row.

**Absolute fetching functions**

- `FIRST_VALUE()` — Retrieves the first value in the window.
- `LAST_VALUE()` — Retrieves the last value in the window.

Their results are based on the boundaries of the window rather than the current row's relative position.

## 3. LEAD()

The `LEAD()` function retrieves a value from a following row.

It is similar to `LAG()`, but instead of looking backward, it looks forward.

### Syntax

```sql
LEAD(column_name, n) OVER (
    ORDER BY column_name
)
```

- `column_name` — The column containing the value to retrieve.
- `n` — The number of rows to look forward.
- `ORDER BY` — Determines the sequence of rows.

If `n` is omitted, the default offset is `1`.

### Example: Retrieving the Next Olympic Host Cities

```sql
SELECT
    Year,
    City,
    -- Retrieve the next Olympic host city
    LEAD(City, 1) OVER (
        ORDER BY Year ASC
    ) AS Next_City,
    -- Retrieve the host city two rows ahead
    LEAD(City, 2) OVER (
        ORDER BY Year ASC
    ) AS After_Next_City
FROM (
    SELECT DISTINCT
        Year,
        City
    FROM Summer_Medals
) AS Host_Cities
ORDER BY Year ASC;
```

### Explanation

- `LEAD(City, 1)` — Retrieves the city from the next row.
- `LEAD(City, 2)` — Retrieves the city two rows after the current row.
- `ORDER BY Year ASC` — Arranges the Olympic host cities chronologically.
- `AS Next_City` — Names the column containing the next host city.
- `AS After_Next_City` — Names the column containing the host city two rows ahead.

### Example Output

| Year | City | Next_City | After_Next_City |
|---:|---|---|---|
| 2004 | Athens | Beijing | London |
| 2008 | Beijing | London | NULL |
| 2012 | London | NULL | NULL |

*The output is illustrative.*

**Important:** `LEAD()` returns `NULL` when there is no following row at the requested offset.

For example:
- The last row has no next city.
- The second-to-last row has no city two rows ahead.

## 4. FIRST_VALUE() and LAST_VALUE()

Unlike `LAG()` and `LEAD()`, which retrieve values relative to the current row, `FIRST_VALUE()` and `LAST_VALUE()` retrieve values from the beginning or end of a window.

### FIRST_VALUE()

Returns the first value in the specified window.

**Syntax:**

```sql
FIRST_VALUE(column_name) OVER (
    ORDER BY column_name
)
```

### LAST_VALUE()

Returns the last value in the specified window.

**Syntax:**

```sql
LAST_VALUE(column_name) OVER (
    ORDER BY column_name
    RANGE BETWEEN UNBOUNDED PRECEDING
    AND UNBOUNDED FOLLOWING
)
```

### Example: Retrieving the First and Last Olympic Host Cities

```sql
SELECT
    Year,
    City,
    -- Get the first Olympic host city
    FIRST_VALUE(City) OVER (
        ORDER BY Year ASC
    ) AS First_City,
    -- Get the last Olympic host city
    LAST_VALUE(City) OVER (
        ORDER BY Year ASC
        RANGE BETWEEN UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING
    ) AS Last_City
FROM (
    SELECT DISTINCT
        Year,
        City
    FROM Summer_Medals
) AS Host_Cities
ORDER BY Year ASC;
```

### Explanation

**FIRST_VALUE(City)**

- Retrieves the first city based on the specified ordering.
- Since the data is ordered by year in ascending order, the first city is Athens.

**LAST_VALUE(City)**

- Retrieves the last city based on the specified window.
- The additional `RANGE BETWEEN` clause extends the window to include all rows, allowing the function to retrieve the actual final city.

### Understanding the Window Frame

```sql
RANGE BETWEEN UNBOUNDED PRECEDING
AND UNBOUNDED FOLLOWING
```

This defines the boundaries of the window:

| Clause | Meaning |
|---|---|
| `RANGE` | Defines a window frame based on the ordering values. |
| `UNBOUNDED PRECEDING` | Starts at the first row of the partition. |
| `UNBOUNDED FOLLOWING` | Extends to the last row of the partition. |

**Why is this important?**

By default, when an `ORDER BY` is specified, the window frame commonly ends at the current row (including its ordering peers). Therefore, `LAST_VALUE()` may return the current row's value rather than the final value in the entire partition.

Adding the full window frame ensures that the function can access the actual last value.

## 5. Partitioning with LEAD()

Fetching functions can also be combined with `PARTITION BY`.

Consider a dataset containing champions from two athletics events:

- Discus Throw
- Triple Jump

If you use `LEAD()` without partitioning, the function processes both events as one continuous sequence.

This can produce incorrect comparisons because the last Discus Throw champion might retrieve the first Triple Jump champion as the next champion.

### Example Without PARTITION BY

```sql
SELECT
    Year,
    Event,
    Country AS Champion,
    LEAD(Country, 1) OVER (
        ORDER BY Year ASC
    ) AS Next_Champion
FROM Summer_Medals
WHERE
    Sport = 'Athletics'
    AND Event IN ('Discus Throw', 'Triple Jump')
    AND Gender = 'Men'
    AND Medal = 'Gold'
ORDER BY Year ASC;
```

### Correcting the Query with PARTITION BY

```sql
SELECT
    Year,
    Event,
    Country AS Champion,
    LEAD(Country, 1) OVER (
        PARTITION BY Event
        ORDER BY Year ASC
    ) AS Next_Champion
FROM Summer_Medals
WHERE
    Sport = 'Athletics'
    AND Event IN ('Discus Throw', 'Triple Jump')
    AND Gender = 'Men'
    AND Medal = 'Gold'
ORDER BY Event ASC, Year ASC;
```

### Explanation

- `PARTITION BY Event` — Separates Discus Throw and Triple Jump into independent partitions.
- `ORDER BY Year ASC` — Arranges the records chronologically within each event.
- `LEAD(Country, 1)` — Retrieves the next champion within the same event.

**Result:** The last Discus Throw record will return `NULL` for `Next_Champion` if there is no following Discus Throw record. It will not retrieve a Triple Jump champion.

## 6. Partitioning with FIRST_VALUE()

The same principle applies to `FIRST_VALUE()` and `LAST_VALUE()`.

Without partitioning, the first value may come from a different event.

For example, if the dataset contains Discus Throw and Triple Jump champions, the first champion in the entire table might be returned for both events.

To retrieve the first champion separately for each event, use `PARTITION BY Event`.

### Example: FIRST_VALUE() with PARTITION BY

```sql
SELECT
    Year,
    Event,
    Country AS Champion,
    FIRST_VALUE(Country) OVER (
        PARTITION BY Event
        ORDER BY Year ASC
    ) AS First_Champion
FROM Summer_Medals
WHERE
    Sport = 'Athletics'
    AND Event IN ('Discus Throw', 'Triple Jump')
    AND Gender = 'Men'
    AND Medal = 'Gold'
ORDER BY Event ASC, Year ASC;
```

### Example: LAST_VALUE() with PARTITION BY

```sql
SELECT
    Year,
    Event,
    Country AS Champion,
    LAST_VALUE(Country) OVER (
        PARTITION BY Event
        ORDER BY Year ASC
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING
    ) AS Last_Champion
FROM Summer_Medals
WHERE
    Sport = 'Athletics'
    AND Event IN ('Discus Throw', 'Triple Jump')
    AND Gender = 'Men'
    AND Medal = 'Gold'
ORDER BY Event ASC, Year ASC;
```

### Explanation

- `PARTITION BY Event` — Creates a separate window for each event.
- `FIRST_VALUE(Country)` — Retrieves the first champion within each event.
- `LAST_VALUE(Country)` — Retrieves the last champion within each event.
- `ORDER BY Year ASC` — Establishes the chronological sequence.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING` — Extends the window frame from the first row to the last row of the partition.

**Key takeaway:** Partitioning ensures that the fetching functions retrieve values only from the appropriate group.

## 7. Key Takeaways

| Function | What it retrieves | Example |
|---|---|---|
| `LAG()` | Previous row's value | Previous year's champion |
| `LEAD()` | Next row's value | Next Olympic host city |
| `FIRST_VALUE()` | First value in the window | First Olympic host city |
| `LAST_VALUE()` | Last value in the window | Last Olympic host city |

### Important Concepts to Remember

1. **Relative fetching:** `LAG()` and `LEAD()` retrieve values based on the current row's position.
2. **Absolute fetching:** `FIRST_VALUE()` and `LAST_VALUE()` retrieve values based on the window's boundaries.
3. **PARTITION BY:** Separates records into independent groups so that values from unrelated groups are not mixed.
4. **ORDER BY:** Determines the sequence in which rows are considered.
5. **Window frames:** Define which rows are included in a window calculation, particularly important when using `LAST_VALUE()`.

**Remember these four functions:**

- `LAG()` — Look backward.
- `LEAD()` — Look forward.
- `FIRST_VALUE()` — Get the first value.
- `LAST_VALUE()` — Get the last value.
