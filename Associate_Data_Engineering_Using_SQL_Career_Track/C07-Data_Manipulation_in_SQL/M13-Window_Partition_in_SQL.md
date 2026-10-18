# 🪟 Window Partitions in SQL

## 1. Window Partitions

You've learned how to use the `OVER()` clause with aggregate functions and ranking functions.

The next step is learning how to use **`PARTITION BY`** inside the `OVER()` clause.

`PARTITION BY` allows you to calculate separate values for different categories while keeping the individual rows in the result set.

For example, you can calculate:
- Average goals per season
- Average goals per country
- Average goals per country and season
- Rankings within each season or country

### 🧠 Key concept

    OVER()
    → Calculate across the entire result set

    OVER(PARTITION BY column)
    → Calculate separately for each category

---

## 2. OVER and PARTITION BY

The `PARTITION BY` clause divides the result set into groups based on one or more columns.

Unlike `GROUP BY`, it does not collapse each group into a single row.

### Basic syntax

    AGGREGATE_FUNCTION(column) OVER (
        PARTITION BY column
    )

### Example: Average home goals per season

    SELECT
        season,
        home_goal,
        AVG(home_goal) OVER (
            PARTITION BY season
        ) AS season_avg
    FROM match;

### Explanation

- `AVG(home_goal)` calculates the average home goals.
- `OVER()` specifies the window calculation.
- `PARTITION BY season` separates matches by season.
- `AS season_avg` names the calculated column.

The average is calculated separately for each season and displayed on every row belonging to that season.

### 🧠 Mental model

    Read the season
        ↓
    Find all matches in that season
        ↓
    Calculate that season's average
        ↓
    Display the average on every matching row

---

## 3. Partition Your Data

Let's revisit the earlier question:

> How many goals were scored in each match, and how did that compare to the overall average?

We can use a window function to calculate the average total goals across all rows.

### Overall average

    SELECT
        date,
        season,
        home_goal,
        away_goal,
        AVG(home_goal + away_goal) OVER () AS overall_avg
    FROM match;

Here, `OVER()` has no `PARTITION BY` clause, so the average is calculated across the entire result set produced by the query.

Every match receives the same `overall_avg` value.

### The next question

> How many goals were scored in each match, and how did that compare to the average for that season?

We can answer this by adding `PARTITION BY season`.

    SELECT
        date,
        season,
        home_goal,
        away_goal,
        AVG(home_goal + away_goal) OVER (
            PARTITION BY season
        ) AS season_avg
    FROM match;

### What's different?

The calculation now uses the season as the partition.

| season | home_goal | away_goal | season_avg |
|---|---:|---:|---:|
| 2011/2012 | 2 | 1 | 2.74 |
| 2011/2012 | 1 | 1 | 2.74 |
| 2012/2013 | 3 | 2 | 2.76 |
| 2012/2013 | 0 | 1 | 2.76 |

*The numbers are illustrative, not actual calculated results.*

Notice that:
- The first two matches belong to `2011/2012`, so they share that season's average.
- The next two matches belong to `2012/2013`, so they share a different average.
- Every individual match remains in the result set.

### ⭐ Important distinction

    AVG(home_goal + away_goal) OVER ()

Calculates one overall average across the result set.

    AVG(home_goal + away_goal) OVER (
        PARTITION BY season
    )

Calculates a separate average for each season.

---

## 4. PARTITION BY Multiple Columns

You can partition data using more than one column.

For example, suppose you want to calculate average total goals for each **country in each season**.

Use:

    PARTITION BY season, country

### Example query

    SELECT
        m.date,
        m.season,
        c.name AS country,
        m.home_goal,
        m.away_goal,
        AVG(m.home_goal + m.away_goal) OVER (
            PARTITION BY m.season, c.name
        ) AS season_country_avg
    FROM match AS m
    LEFT JOIN country AS c
        ON m.country_id = c.id;

### Explanation

The window function:

    AVG(m.home_goal + m.away_goal) OVER (
        PARTITION BY m.season, c.name
    )

calculates average total goals separately for every combination of season and country.

For example:

| season | country | home_goal | away_goal | season_country_avg |
|---|---|---:|---:|---:|
| 2011/2012 | Belgium | 1 | 0 | 2.88 |
| 2011/2012 | Belgium | 2 | 1 | 2.88 |
| 2011/2012 | France | 3 | 2 | 2.65 |
| 2011/2012 | France | 1 | 1 | 2.65 |
| 2012/2013 | Belgium | 0 | 0 | 2.70 |

*The averages are illustrative.*

### How the partition works

The database calculates separate averages for combinations such as:

- Belgium + 2011/2012
- France + 2011/2012
- Belgium + 2012/2013
- France + 2012/2013

Each match is compared with the average for its own country and season.

### 🧠 Mental model

    PARTITION BY season, country
        ↓
    Group rows by season AND country
        ↓
    Calculate the average within each combination
        ↓
    Keep all original rows

**Important:** The order of columns in `PARTITION BY` does not change which combinations define the partitions.

---

## 5. PARTITION BY Considerations

`PARTITION BY` is a flexible addition to the `OVER()` clause.

You can partition calculations by one or more columns, depending on the question you want to answer.

### 5.1 You can partition by one column

    AVG(home_goal) OVER (
        PARTITION BY season
    )

Calculates average home goals per season.

### 5.2 You can partition by multiple columns

    AVG(home_goal + away_goal) OVER (
        PARTITION BY season, country_id
    )

Calculates average total goals for each country in each season.

### 5.3 You can use PARTITION BY with ranking functions

For example, rank matches separately within each season:

    SELECT
        season,
        date,
        home_goal,
        away_goal,
        RANK() OVER (
            PARTITION BY season
            ORDER BY home_goal + away_goal DESC
        ) AS season_rank
    FROM match;

This assigns Rank 1 to the highest-scoring match or matches within each season.

When the season changes, the ranking starts again.

### 5.4 PARTITION BY is different from GROUP BY

| Feature | `GROUP BY` | `PARTITION BY` |
|---|---|---|
| Groups rows for calculations | ✅ Yes | ✅ Yes |
| Usually reduces the number of rows | ✅ Yes | ❌ No |
| Keeps individual match details | Not by itself | ✅ Yes |
| Can calculate averages per season | ✅ Yes | ✅ Yes |

### Example using GROUP BY

    SELECT
        season,
        AVG(home_goal + away_goal) AS season_avg
    FROM match
    GROUP BY season;

This returns one row per season.

### Example using PARTITION BY

    SELECT
        season,
        date,
        home_goal,
        away_goal,
        AVG(home_goal + away_goal) OVER (
            PARTITION BY season
        ) AS season_avg
    FROM match;

This returns individual matches with the corresponding season average.

---

## 6. Let's Practice! 🎯

You are now ready to practice window partitions using the `match` dataset.

Remember these three patterns:

### Overall average

    AVG(home_goal + away_goal) OVER ()

### Average per season

    AVG(home_goal + away_goal) OVER (
        PARTITION BY season
    )

### Average per country and season

    AVG(home_goal + away_goal) OVER (
        PARTITION BY country_id, season
    )

### Rank matches within each season

    RANK() OVER (
        PARTITION BY season
        ORDER BY home_goal + away_goal DESC
    )

---

## 🔑 Key Takeaways

1. **`OVER()`** defines the window used for a window function.
2. **`PARTITION BY`** divides the result set into categories for separate calculations.
3. You can partition by one column or multiple columns.
4. Window partitions keep the individual rows in the result set.
5. `PARTITION BY` works with aggregate functions, ranking functions, and other window functions.
6. Use `GROUP BY` when you want summarized rows; use `PARTITION BY` when you want calculations for each group while retaining row-level details.

### 🧠 Quick mental model

    OVER()
    → One calculation across the result set

    OVER(PARTITION BY season)
    → One calculation per season

    OVER(PARTITION BY season, country)
    → One calculation per season-country combination

    OVER(
        PARTITION BY season
        ORDER BY total_goals DESC
    )
    → Rank or order values within each season
