# SQL Window Functions — ORDER BY

## 1. ORDER BY

In the previous lesson, you learned the basics of window functions. In this lesson, you will learn about `ORDER BY`, one of the subclauses used within the `OVER()` clause.

The `ORDER BY` inside `OVER()` determines the order in which a window function processes rows.

## 2. Row Numbers

Recall the previous query that assigned a number to each row using `ROW_NUMBER()`.

```sql
SELECT
    Year,
    ROW_NUMBER() OVER() AS Row_N
FROM Summer_Medals;
```

The first row receives number `1`, the second receives `2`, and so on.

What if you want to reverse the numbering so that the most recent year receives `1` and the oldest year receives the highest number?

You can do this by adding `ORDER BY Year DESC` inside `OVER()`.

## 3. Using ORDER BY Inside OVER()

```sql
SELECT
    Year,
    ROW_NUMBER() OVER(
        ORDER BY Year DESC
    ) AS Row_N
FROM Summer_Medals
GROUP BY Year
ORDER BY Year DESC;
```

### Explanation

- `ROW_NUMBER()` — Assigns a unique sequential number to each row.
- `OVER(ORDER BY Year DESC)` — Numbers rows based on the year, starting with the most recent year.
- `GROUP BY Year` — Produces one row per year.
- `ORDER BY Year DESC` — Displays the final results from the most recent year to the oldest.

For example, if the dataset contains 2012, 2008, and 2004, the row numbers would be:

| Year | Row_N |
|---:|---:|
| 2012 | 1 |
| 2008 | 2 |
| 2004 | 3 |

**Important:** The `ORDER BY` inside `OVER()` controls how the row numbers are assigned. The outer `ORDER BY` controls how the final results are displayed.

## 4. Ordering by Multiple Columns

You can order rows by more than one column inside `OVER()`. For example, you can order Olympic medal records by year and then by event.

```sql
SELECT
    Year,
    Event,
    ROW_NUMBER() OVER(
        ORDER BY Year ASC, Event ASC
    ) AS Row_N
FROM Summer_Medals
ORDER BY Year ASC, Event ASC;
```

### Explanation

- `ORDER BY Year ASC, Event ASC` inside `OVER()` — Assigns row numbers by year, then alphabetically by event when years are equal.
- `ORDER BY Year ASC, Event ASC` outside `OVER()` — Displays the results using the same sorting rules.

You can use multiple columns to establish a more specific ordering for the rows.

## 5. Ordering Inside and Outside OVER()

You can use different ordering rules inside and outside `OVER()` in the same query.

```sql
SELECT
    Country,
    Year,
    Event,
    ROW_NUMBER() OVER(
        ORDER BY Year ASC, Event ASC
    ) AS Row_N
FROM Summer_Medals
ORDER BY Country ASC, Row_N ASC;
```

### How SQL Processes the Ordering

1. **Inside `OVER()`** — `ROW_NUMBER()` assigns numbers based on `Year` and `Event`.
2. **Outside `OVER()`** — SQL displays the numbered results ordered by `Country` and then `Row_N`.

The first row displayed does not necessarily have `Row_N = 1`, because the final display order may differ from the order used to assign the row numbers.

**Key takeaway:** The inner `ORDER BY` determines numbering; the outer `ORDER BY` determines presentation.

## 6. Determining the Reigning Champion

A reigning champion is an athlete or team that wins a competition in consecutive editions or years.

To identify reigning champions, you need to compare the current champion with the champion from the previous year. Window functions make this possible without requiring a complex self-join.

The `LAG()` function retrieves a value from a previous row.

### Syntax

```sql
LAG(column_name, n) OVER(
    ORDER BY column_name
)
```

- `column_name` — The column containing the value to retrieve.
- `n` — The number of rows to look backward.
- `ORDER BY` — Determines the order in which rows are considered.

For example, `LAG(Champion, 1)` retrieves the champion from the previous row.

## 7. Retrieving Current Champions

First, retrieve the champions of the Discus Throw event.

```sql
SELECT
    Year,
    Country AS Champion
FROM Summer_Medals
WHERE
    Sport = 'Athletics'
    AND Event = 'Discus Throw'
    AND Gender = 'Men'
    AND Medal = 'Gold'
ORDER BY Year ASC;
```

This query identifies the gold medal-winning country for each matching year. The result provides the current champions needed for comparison.

*Note:* This assumes the dataset represents the champion by the country winning the gold medal. If multiple athletes from the same country win medals in a team event, additional handling may be needed.

## 8. Comparing Current and Previous Champions with LAG()

Use a Common Table Expression (CTE) to store the champion query temporarily, then use `LAG()` to retrieve the previous champion.

```sql
WITH Discus_Gold AS (
    SELECT
        Year,
        Country AS Champion
    FROM Summer_Medals
    WHERE
        Sport = 'Athletics'
        AND Event = 'Discus Throw'
        AND Gender = 'Men'
        AND Medal = 'Gold'
)
SELECT
    Year,
    Champion,
    LAG(Champion, 1) OVER(
        ORDER BY Year ASC
    ) AS Last_Champion
FROM Discus_Gold
ORDER BY Year ASC;
```

### Explanation

- `WITH Discus_Gold AS (...)` — Creates a CTE containing the year and champion for the selected event.
- `LAG(Champion, 1)` — Retrieves the champion from the previous row.
- `OVER(ORDER BY Year ASC)` — Orders the rows chronologically so the previous row represents the previous recorded Olympic year.
- `AS Last_Champion` — Names the column containing the previous champion.
- `ORDER BY Year ASC` — Displays the results from earliest to latest.

Example of the expected output structure:

| Year | Champion | Last_Champion |
|---:|---|---|
| 2000 | Country A | NULL |
| 2004 | Country B | Country A |
| 2008 | Country B | Country B |
| 2012 | Country C | Country B |

*The country names above are illustrative.*

The first row has `NULL` in `Last_Champion` because there is no preceding row.

## 9. Identifying Reigning Champions

Once you have both `Champion` and `Last_Champion`, you can compare them to identify consecutive wins.

```sql
WITH Discus_Gold AS (
    SELECT
        Year,
        Country AS Champion
    FROM Summer_Medals
    WHERE
        Sport = 'Athletics'
        AND Event = 'Discus Throw'
        AND Gender = 'Men'
        AND Medal = 'Gold'
),
Champion_History AS (
    SELECT
        Year,
        Champion,
        LAG(Champion, 1) OVER(
            ORDER BY Year ASC
        ) AS Last_Champion
    FROM Discus_Gold
)
SELECT
    Year,
    Champion,
    Last_Champion,
    CASE
        WHEN Champion = Last_Champion THEN 'Reigning Champion'
        ELSE 'New Champion'
    END AS Champion_Status
FROM Champion_History
ORDER BY Year ASC;
```

This additional query compares each champion with the previous row's champion. Matching values indicate that the same country won in consecutive recorded editions.

**Important:** The example compares countries, not individual athletes. Also, `LAG()` compares the previous available row, so it does not by itself verify that the wins occurred in consecutive Olympic editions if the event is missing from some years.

## 10. Key Takeaways

| Function or clause | Purpose |
|---|---|
| `ROW_NUMBER()` | Assigns a unique sequential number to each row |
| `OVER(ORDER BY ...)` | Controls the order used by the window function |
| `ORDER BY` outside `OVER()` | Controls the final display order |
| Multiple columns in `ORDER BY` | Establishes a more specific sorting order |
| `LAG(column, 1)` | Retrieves a value from the previous row |
| `WITH` (CTE) | Defines a temporary named result set for a query |

**Remember:** Use `ROW_NUMBER()` with `ORDER BY` when numbering must follow a specific sequence, and use `LAG()` when you need to compare the current row with a previous row.
