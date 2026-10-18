# 🪟 PARTITION BY Multiple Columns

The `PARTITION BY` clause can divide a dataset using multiple columns, allowing window functions to calculate separate values for each combination of categories.

For example, you can calculate average goals by:

- Season
- Country
- Season and country
- Season and calendar month

You can also use calculations, such as `EXTRACT(MONTH FROM date)`, to create the categories used for partitioning.

In this exercise, we examine matches involving **Legia Warszawa** and calculate average home and away goals partitioned by **season and month**.

---

## 🎯 Exercise

**Question:** Calculate the average number of home and away goals scored by Legia Warszawa and their opponents, partitioned by month in each season.

**Instructions (100 XP)**

- Construct two window functions partitioning the average of home and away goals by season and month.
- Filter the dataset by Legia Warszawa's team ID (`8673`) so that the window calculation includes only matches involving them.

---

## ✅ Answer

    SELECT
        date,
        season,
        home_goal,
        away_goal,

        CASE
            WHEN hometeam_id = 8673 THEN 'home'
            ELSE 'away'
        END AS warsaw_location,

        -- Calculate average goals partitioned by season and month
        AVG(home_goal) OVER (
            PARTITION BY season, EXTRACT(MONTH FROM date)
        ) AS season_mo_home,

        AVG(away_goal) OVER (
            PARTITION BY season, EXTRACT(MONTH FROM date)
        ) AS season_mo_away

    FROM match

    WHERE
        hometeam_id = 8673
        OR awayteam_id = 8673

    ORDER BY (home_goal + away_goal) DESC;

---

## 🔍 Step-by-Step Explanation

### 1. Select the match details

    SELECT
        date,
        season,
        home_goal,
        away_goal

These columns identify when the match took place, which season it belongs to, and how many goals each team scored.

### 2. Identify Legia Warszawa's location

    CASE
        WHEN hometeam_id = 8673 THEN 'home'
        ELSE 'away'
    END AS warsaw_location

This identifies whether Legia Warszawa played at home or away.

- `home` means Legia Warszawa was the home team.
- `away` means Legia Warszawa was the away team.

The `CASE` expression works because the `WHERE` clause includes only matches involving Legia Warszawa.

### 3. Calculate average home goals by season and month

    AVG(home_goal) OVER (
        PARTITION BY season, EXTRACT(MONTH FROM date)
    ) AS season_mo_home

Let's break this down:

- `AVG(home_goal)` calculates the average number of goals scored by the home team.
- `PARTITION BY season` separates matches by season.
- `EXTRACT(MONTH FROM date)` extracts the calendar month from each match date.
- `season_mo_home` is the name of the calculated column.

For example, matches in August of `2012/2013` belong to one partition, while matches in September of the same season belong to another.

### 4. Calculate average away goals by season and month

    AVG(away_goal) OVER (
        PARTITION BY season, EXTRACT(MONTH FROM date)
    ) AS season_mo_away

This calculates the average goals scored by away teams for each season-month combination.

The difference is the column being averaged:

| Window function | What it calculates |
|---|---|
| `AVG(home_goal)` | Average home-team goals |
| `AVG(away_goal)` | Average away-team goals |

Both functions use the same partitioning logic.

### 5. Filter matches involving Legia Warszawa

    WHERE
        hometeam_id = 8673
        OR awayteam_id = 8673

This keeps matches in which Legia Warszawa was either the home team or the away team.

**Important:** Because `WHERE` is evaluated before window functions, these averages are calculated only from Legia Warszawa's matches, not from all matches played in the league.

### 6. Sort by total goals

    ORDER BY (home_goal + away_goal) DESC;

This sorts the matches from the highest total goals to the lowest.

---

## 🧠 Understanding Multiple Partitions

The expression:

    PARTITION BY season, EXTRACT(MONTH FROM date)

creates a separate partition for each combination of season and calendar month.

For example:

| Season | Month | Partition |
|---|---|---|
| 2012/2013 | August | 2012/2013 + August |
| 2012/2013 | September | 2012/2013 + September |
| 2012/2013 | October | 2012/2013 + October |
| 2013/2014 | August | 2013/2014 + August |

August in two different seasons belongs to two different partitions.

### 🧠 Mental model

    PARTITION BY season, month
            ↓
    Separate matches by season
            ↓
    Separate each season by month
            ↓
    Calculate averages within each partition
            ↓
    Display the averages alongside the matching rows

---

## ⚠️ Important Distinction

The exercise specifically filters the data to Legia Warszawa's matches before calculating the window averages.

Therefore, `season_mo_home` and `season_mo_away` represent averages among **Legia Warszawa's matches for each season and month**.

If you instead want averages for *all matches in the league* for each season and month, calculate the window averages before applying the team filter. For example:

    WITH monthly_averages AS (
        SELECT
            date,
            season,
            home_goal,
            away_goal,
            hometeam_id,
            awayteam_id,
            AVG(home_goal) OVER (
                PARTITION BY season, EXTRACT(MONTH FROM date)
            ) AS season_mo_home,
            AVG(away_goal) OVER (
                PARTITION BY season, EXTRACT(MONTH FROM date)
            ) AS season_mo_away
        FROM match
    )
    SELECT
        date,
        season,
        home_goal,
        away_goal,
        CASE
            WHEN hometeam_id = 8673 THEN 'home'
            ELSE 'away'
        END AS warsaw_location,
        season_mo_home,
        season_mo_away
    FROM monthly_averages
    WHERE
        hometeam_id = 8673
        OR awayteam_id = 8673
    ORDER BY (home_goal + away_goal) DESC;

This version compares Legia Warszawa's matches against the monthly averages across all matches in the database.

---

## 📌 Quick Reference

### Partition by season

    AVG(home_goal) OVER (
        PARTITION BY season
    )

### Partition by season and month

    AVG(home_goal) OVER (
        PARTITION BY season, EXTRACT(MONTH FROM date)
    )

### Partition by season and country

    AVG(home_goal + away_goal) OVER (
        PARTITION BY season, country_id
    )

### Key Takeaways

1. `PARTITION BY` supports multiple columns and expressions.
2. `EXTRACT(MONTH FROM date)` extracts the month number from a date.
3. Each unique season-month combination forms a separate partition.
4. Window functions retain individual rows instead of collapsing them into summaries.
5. The `WHERE` clause determines which rows are available to the window calculation.
6. To compare a team's performance with league-wide averages, calculate the averages before filtering to that team.
