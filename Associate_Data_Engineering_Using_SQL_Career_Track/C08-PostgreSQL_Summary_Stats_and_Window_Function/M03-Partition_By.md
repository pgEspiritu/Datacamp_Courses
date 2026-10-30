# SQL Window Functions — PARTITION BY

## 1. PARTITION BY

You have learned how to change the behavior of a window function using the `ORDER BY` subclause. Another way to control how a window function operates is through the `PARTITION BY` subclause.

`PARTITION BY` divides the rows into separate groups based on the unique values of one or more columns. The window function then operates independently within each group.

## 2. Motivation: Why Do We Need PARTITION BY?

Let's build on the previous example involving Olympic champions.

Suppose you want to retrieve the previous year's champion for two events:
- Discus Throw
- Triple Jump

You can use `LAG()` to retrieve the previous champion. However, without `PARTITION BY`, the function considers all rows as part of one continuous sequence.

### Example Without PARTITION BY

```sql
SELECT
    Year,
    Event,
    Country AS Champion,
    LAG(Country) OVER (
        ORDER BY Year ASC
    ) AS Last_Champion
FROM Summer_Medals
WHERE
    Sport = 'Athletics'
    AND Event IN ('Discus Throw', 'Triple Jump')
    AND Gender = 'Men'
    AND Medal = 'Gold'
ORDER BY Year ASC;
```

The problem is that `LAG()` does not distinguish between the two events.

For example, the first Triple Jump record might retrieve the most recent Discus Throw champion as its `Last_Champion`.

This is incorrect because the champions of different events should be compared separately.

## 3. Introducing PARTITION BY

The `PARTITION BY` subclause solves this problem by dividing the dataset into separate groups.

### Syntax

```sql
FUNCTION_NAME(column_name) OVER (
    PARTITION BY column_name
    ORDER BY column_name
)
```

- `PARTITION BY` — Divides rows into separate groups based on the specified column.
- `ORDER BY` — Determines the order of rows within each partition.
- `FUNCTION_NAME()` — Performs the window function independently within each partition.

### Important Difference: GROUP BY vs. PARTITION BY

| GROUP BY | PARTITION BY |
|---|---|
| Groups rows into summary results. | Divides rows into separate partitions. |
| Usually reduces the number of rows. | Preserves the original rows. |
| Commonly used with aggregate functions such as `SUM()` and `COUNT()`. | Used with window functions such as `ROW_NUMBER()`, `LAG()`, and `RANK()`. |

**Remember:** `GROUP BY` summarizes groups of rows, while `PARTITION BY` keeps individual rows and performs calculations within each group.

## 4. Partitioning by One Column

To fix the previous query, add `PARTITION BY Event` inside the `OVER()` clause.

```sql
SELECT
    Year,
    Event,
    Country AS Champion,
    LAG(Country) OVER (
        PARTITION BY Event
        ORDER BY Year ASC
    ) AS Last_Champion
FROM Summer_Medals
WHERE
    Sport = 'Athletics'
    AND Event IN ('Discus Throw', 'Triple Jump')
    AND Gender = 'Men'
    AND Medal = 'Gold'
ORDER BY Event, Year ASC;
```

### Explanation

- `PARTITION BY Event` — Creates a separate partition for each event.
- `ORDER BY Year ASC` — Arranges the records chronologically within each event.
- `LAG(Country)` — Retrieves the previous champion only from the same event partition.

### Example Output

| Year | Event | Champion | Last_Champion |
|---:|---|---|---|
| 2008 | Discus Throw | Country A | NULL |
| 2012 | Discus Throw | Country B | Country A |
| 2008 | Triple Jump | Country C | NULL |
| 2012 | Triple Jump | Country D | Country C |

*The country names are illustrative.*

Notice that the first record of each event has `NULL` for `Last_Champion`. This is because each event has its own partition, and there is no previous row within that partition.

## 5. More Complex Partitioning

You can also use `PARTITION BY` with multiple columns.

For example, suppose you want to number gold medals awarded to female athletes from China and Japan.

The goal is to number the records separately for each combination of country and year.

Without partitioning, the row numbers would continue across different countries and Olympic years.

## 6. Partitioning by Multiple Columns

To reset row numbering for each country and year, use:

```sql
SELECT
    Year,
    Country,
    Event,
    ROW_NUMBER() OVER (
        PARTITION BY Year, Country
        ORDER BY Event ASC
    ) AS Row_N
FROM Summer_Medals
WHERE
    Country IN ('CHN', 'JPN')
    AND Gender = 'Women'
    AND Medal = 'Gold'
ORDER BY Year ASC, Country ASC, Row_N ASC;
```

### Explanation

- `PARTITION BY Year, Country` — Creates a separate partition for each unique combination of year and country.
- `ORDER BY Event ASC` — Numbers the events alphabetically within each partition.
- `ROW_NUMBER()` — Assigns sequential numbers starting at `1` within each partition.

### How the Partitions Work

Each unique combination of `Year` and `Country` becomes a separate partition.

For example:

| Year | Country | Partition |
|---:|---|---|
| 2008 | CHN | 2008 - CHN |
| 2008 | JPN | 2008 - JPN |
| 2012 | CHN | 2012 - CHN |
| 2012 | JPN | 2012 - JPN |

The row number resets to `1` whenever a new partition begins.

**Key takeaway:** You can partition by multiple columns when you need to reset a window function based on more than one grouping condition.

## 7. Key Takeaways

| Window function concept | Purpose |
|---|---|
| `ORDER BY` | Determines the order in which rows are processed by the window function. |
| `PARTITION BY` | Divides rows into separate groups for independent window calculations. |
| `PARTITION BY Event` | Separates calculations by event. |
| `PARTITION BY Year, Country` | Separates calculations by each year-and-country combination. |
| `ROW_NUMBER()` | Assigns sequential numbers within each partition. |
| `LAG()` | Retrieves a value from a previous row within the same partition. |

### Remember the Difference

- **ORDER BY:** In what order should the window function process the rows?
- **PARTITION BY:** Which rows should be processed together?

You can combine both subclauses to control how window functions operate within specific groups and sequences.
