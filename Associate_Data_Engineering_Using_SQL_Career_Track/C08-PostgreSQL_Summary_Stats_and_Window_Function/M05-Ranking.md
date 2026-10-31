# SQL Window Functions: Ranking

## 1. Introduction to Ranking

Another common application of SQL window functions is **ranking rows according to their values**.

Ranking functions allow us to assign positions to records based on a specified order, such as:
- Countries ranked by the number of Olympic Games they participated in.
- Athletes ranked by the number of medals they earned.
- Employees ranked by their salaries.
- Products ranked by sales performance.

SQL provides three commonly used ranking functions:

1. `ROW_NUMBER()`
2. `RANK()`
3. `DENSE_RANK()`

## 2. The Three Ranking Functions

Although all three functions assign rankings, they handle tied values differently.

### A. ROW_NUMBER()

`ROW_NUMBER()` assigns a unique sequential number to every row, even when multiple rows have the same value.

**Example:**

| Country | Games Participated | ROW_NUMBER |
|---|---:|---:|
| USA | 28 | 1 |
| Denmark | 27 | 2 |
| France | 27 | 3 |
| Italy | 26 | 4 |
| China | 25 | 5 |

Notice that Denmark and France have the same number of participations, but they receive different row numbers.

The order between tied rows is not guaranteed unless you specify an additional tie-breaker.

### B. RANK()

`RANK()` assigns the same rank to rows with identical values. However, it skips the next rank or ranks after a tie.

**Example:**

| Country | Games Participated | RANK |
|---|---:|---:|
| USA | 28 | 1 |
| Denmark | 27 | 2 |
| France | 27 | 2 |
| Italy | 26 | 4 |
| China | 25 | 5 |

Denmark and France both receive rank 2 because they have the same number of participations.

However, the next country, Italy, receives rank 4 instead of rank 3.

**Important:** `RANK()` skips rankings after ties.

### C. DENSE_RANK()

`DENSE_RANK()` also assigns the same rank to rows with identical values, but it does not skip the next rank.

**Example:**

| Country | Games Participated | DENSE_RANK |
|---|---:|---:|
| USA | 28 | 1 |
| Denmark | 27 | 2 |
| France | 27 | 2 |
| Italy | 26 | 3 |
| China | 25 | 4 |

Unlike `RANK()`, `DENSE_RANK()` assigns rank 3 to Italy after Denmark and France share rank 2.

**Important:** `DENSE_RANK()` never skips rankings after ties.

## 3. Comparison of the Three Ranking Functions

Using the same dataset, let's compare their results:

| Country | Participations | ROW_NUMBER | RANK | DENSE_RANK |
|---|---:|---:|---:|---:|
| USA | 28 | 1 | 1 | 1 |
| Denmark | 27 | 2 | 2 | 2 |
| France | 27 | 3 | 2 | 2 |
| Italy | 26 | 4 | 4 | 3 |
| China | 25 | 5 | 5 | 4 |

### Key Differences

| Function | Handles ties | Skips ranks? | Ranking behavior |
|---|---|---|---|
| `ROW_NUMBER()` | Assigns unique numbers | No | Every row gets a different number |
| `RANK()` | Assigns the same rank | Yes | Leaves gaps after ties |
| `DENSE_RANK()` | Assigns the same rank | No | Continues without gaps |

**Remember:**
- `ROW_NUMBER()` = Unique numbering.
- `RANK()` = Ties with gaps.
- `DENSE_RANK()` = Ties without gaps.

## 4. Ranking Without Partitioning

Sometimes, we need to rank records belonging to different groups.

For example, suppose we want to rank athletes from China and Russia based on the number of medals they have earned.

Consider this sample dataset:

| Country | Athlete | Medals |
|---|---|---:|
| China | Athlete A | 5 |
| China | Athlete B | 3 |
| Russia | Athlete C | 4 |
| Russia | Athlete D | 2 |
| China | Athlete E | 2 |
| Russia | Athlete F | 2 |

If we rank all athletes without partitioning, SQL ranks everyone relative to the entire result set.

```sql
SELECT
    Country,
    Athlete,
    COUNT(*) AS Medals,
    RANK() OVER (
        ORDER BY COUNT(*) DESC
    ) AS Athlete_Rank
FROM Summer_Medals
WHERE Country IN ('CHN', 'RUS')
GROUP BY Country, Athlete
ORDER BY Country ASC, Medals DESC;
```

*Note: This is an illustrative query. The country codes and dataset values should match the actual records in your database.*

The ranking is calculated across all athletes, regardless of their country.

For example, an athlete from Russia with two medals may receive rank 3 or 4 globally, even if that athlete should be ranked second among Russian athletes.

The outer `ORDER BY Country ASC, Medals DESC` only changes how the results are displayed. It does not change how the ranking function calculates the ranks.

## 5. Ranking With Partitioning

To rank athletes separately within each country, use `PARTITION BY`.

```sql
SELECT
    Country,
    Athlete,
    COUNT(*) AS Medals,
    RANK() OVER (
        PARTITION BY Country
        ORDER BY COUNT(*) DESC
    ) AS Athlete_Rank
FROM Summer_Medals
WHERE Country IN ('CHN', 'RUS')
GROUP BY Country, Athlete
ORDER BY Country ASC, Medals DESC;
```

### Understanding the Query

- `PARTITION BY Country` divides the results into separate groups based on country.
- `ORDER BY COUNT(*) DESC` ranks athletes according to their medal counts, from highest to lowest.
- `RANK()` assigns the ranking within each country independently.
- The final `ORDER BY` controls the display order of the results.

### Expected Output Concept

| Country | Athlete | Medals | Athlete_Rank |
|---|---|---:|---:|
| China | Athlete A | 5 | 1 |
| China | Athlete B | 3 | 2 |
| China | Athlete E | 2 | 3 |
| Russia | Athlete C | 4 | 1 |
| Russia | Athlete D | 2 | 2 |
| Russia | Athlete F | 2 | 2 |

The ranking restarts at 1 for each country.

In this example, Athlete D and Athlete F both receive rank 2 because they have the same number of medals.

## 6. Understanding PARTITION BY in Ranking Functions

The `PARTITION BY` clause divides the result set into smaller groups before applying the ranking function.

For example:

```sql
RANK() OVER (
    PARTITION BY Country
    ORDER BY Medals DESC
)
```

This means:
1. Divide the records according to `Country`.
2. Within each country, sort athletes by their medal counts in descending order.
3. Assign rankings separately within each country.

You can also partition using multiple columns:

```sql
RANK() OVER (
    PARTITION BY Country, Gender
    ORDER BY Medals DESC
)
```

This creates separate ranking groups for each country-and-gender combination.

## 7. Key Takeaways

- Ranking functions assign positions to rows based on specified values.
- `ROW_NUMBER()` always assigns unique sequential numbers.
- `RANK()` assigns equal rankings to tied values and skips subsequent ranks.
- `DENSE_RANK()` assigns equal rankings to tied values without skipping ranks.
- `PARTITION BY` allows you to rank records independently within groups.
- The `ORDER BY` inside `OVER()` determines the ranking sequence.
- The outer `ORDER BY` determines the final display sequence.

**Remember:** If you want to rank records separately by country, department, gender, or another category, use `PARTITION BY` inside the window function.
