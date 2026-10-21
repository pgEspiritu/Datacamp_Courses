# Lesson Summary: Bringing It All Together — SQL

## 1. Lesson Overview

This lesson reviews the key SQL concepts learned throughout the course and combines them in a case study using the European Soccer Database.

**Case study question:** Who defeated Manchester United in the 2013/2014 season?

The lesson combines `CASE` statements, subqueries, Common Table Expressions (CTEs), and window functions to analyze match results and identify Manchester United's defeats.

## 2. Key SQL Concepts Reviewed

### A. CASE Statements

The `CASE` statement categorizes data based on specified conditions, similar to an if-else statement in programming.

```sql
SELECT
    date,
    home_goal,
    away_goal,
    CASE
        WHEN home_goal > away_goal THEN 'Home Win'
        WHEN home_goal < away_goal THEN 'Away Win'
        ELSE 'Draw'
    END AS match_result
FROM match;
```

**Explanation:**
- `WHEN` specifies a condition.
- `THEN` returns a value when the condition is true.
- `ELSE` handles cases that do not satisfy the preceding conditions.
- `END` closes the `CASE` statement.
- `AS match_result` names the resulting column.

### B. Subqueries

A subquery is a query nested inside another SQL query. It can be used in `SELECT`, `FROM`, or `WHERE` clauses.

Example using a subquery in `WHERE`:

```sql
SELECT
    team_long_name
FROM team
WHERE team_api_id IN (
    SELECT home_team_api_id
    FROM match
    WHERE home_goal > away_goal
);
```

**Explanation:**

The inner query identifies home-team IDs from matches in which the home team won. The outer query retrieves the corresponding team names.

### C. Common Table Expressions (CTEs)

A CTE creates a temporary named result set that can be referenced by the main query. It helps organize complex queries into readable steps.

```sql
WITH home AS (
    SELECT
        match.id,
        match.date,
        team.team_long_name AS home_team
    FROM match
    JOIN team
        ON match.home_team_api_id = team.team_api_id
)
SELECT *
FROM home;
```

**Explanation:**
- `WITH home AS (...)` defines a CTE named `home`.
- The `JOIN` connects match records with team information.
- The main query retrieves the result from the CTE.

CTEs are particularly useful when a query requires several preparation steps or when intermediate results need to be reused.

### D. Window Functions

Window functions calculate values across related rows without collapsing those rows into a single result.

Example using `RANK()`:

```sql
SELECT
    date,
    home_goal,
    away_goal,
    RANK() OVER (
        ORDER BY ABS(home_goal - away_goal) DESC
    ) AS goal_difference_rank
FROM match;
```

**Explanation:**
- `RANK()` assigns a ranking to each row.
- `OVER()` defines the window used for the calculation.
- `ORDER BY` determines the ranking order.
- `ABS(home_goal - away_goal)` calculates the absolute goal difference.

This example ranks matches by the size of the goal difference, from largest to smallest. It does not specifically rank Manchester United's defeats; additional filtering or categorization is needed for that purpose.

## 3. Case Study: Who Defeated Manchester United?

To answer the case study question, we need to:

1. Identify Manchester United's team ID.
2. Retrieve matches from the 2013/2014 season.
3. Determine whether Manchester United played at home or away.
4. Identify matches in which Manchester United lost.
5. Retrieve the names of the opposing teams.
6. Rank the defeats by goal difference.

### Step 1: Identify Manchester United's Team ID

```sql
SELECT
    team_api_id,
    team_long_name
FROM team
WHERE team_long_name = 'Manchester United';
```

This query retrieves Manchester United's team ID. Use the returned ID in the following query.

### Step 2: Identify Manchester United's Defeats

The following example assumes Manchester United's `team_api_id` is `10260`, as commonly used in the European Soccer Database.

```sql
WITH match_results AS (
    SELECT
        m.id,
        m.date,
        m.home_team_api_id,
        m.away_team_api_id,
        m.home_goal,
        m.away_goal,

        CASE
            WHEN m.home_team_api_id = 10260
                 AND m.home_goal < m.away_goal
                THEN 'Loss'

            WHEN m.away_team_api_id = 10260
                 AND m.away_goal < m.home_goal
                THEN 'Loss'

            WHEN m.home_goal = m.away_goal
                THEN 'Draw'

            ELSE 'Win'
        END AS manchester_united_result,

        CASE
            WHEN m.home_team_api_id = 10260
                THEN m.away_team_api_id
            ELSE m.home_team_api_id
        END AS opponent_team_api_id,

        CASE
            WHEN m.home_team_api_id = 10260
                THEN m.away_goal - m.home_goal
            ELSE m.home_goal - m.away_goal
        END AS defeat_goal_difference

    FROM match AS m
    WHERE m.season = '2013/2014'
      AND (
          m.home_team_api_id = 10260
          OR m.away_team_api_id = 10260
      )
),
defeats AS (
    SELECT *
    FROM match_results
    WHERE manchester_united_result = 'Loss'
)
SELECT
    d.date,
    t.team_long_name AS opponent,
    d.home_goal,
    d.away_goal,
    d.defeat_goal_difference,
    RANK() OVER (
        ORDER BY d.defeat_goal_difference DESC
    ) AS defeat_rank
FROM defeats AS d
JOIN team AS t
    ON d.opponent_team_api_id = t.team_api_id
ORDER BY
    defeat_rank,
    d.date;
```

**How the query works:**

- **`match_results` CTE:** Retrieves Manchester United's matches during the specified season, determines the result from Manchester United's perspective, identifies the opponent, and calculates the goal difference.
- **`CASE` statements:** Account for Manchester United playing either at home or away. A loss is identified when Manchester United scores fewer goals than its opponent.
- **`defeats` CTE:** Filters the match results to include only losses.
- **`JOIN team`:** Retrieves the opposing team's name.
- **`RANK()`:** Ranks defeats by goal difference, placing the largest defeat first.
- **`ORDER BY`:** Displays the most significant defeats first, with the match date used to organize tied rankings.

**Important:** This query assumes the standard European Soccer Database schema, including the `match` and `team` tables and the team ID shown above. Verify the team ID against your database before running it.

## 4. Final Takeaways

| SQL concept | Purpose |
|---|---|
| `CASE` | Categorizes match outcomes and calculates conditional values. |
| Subqueries | Nest queries to filter or retrieve data based on another query. |
| CTEs (`WITH`) | Divide complex queries into logical, readable steps. |
| `JOIN` | Combines related information from different tables. |
| Window functions | Calculate rankings or other values across rows without collapsing the results. |
| `RANK()` | Ranks matches based on their goal differences. |
| `WHERE` | Filters records to the required season and team. |

**Overall lesson:** Combining these SQL techniques allows you to transform raw match data into meaningful information and answer analytical questions, such as identifying which teams defeated Manchester United during a particular season.
