# 🧠 CASE Statements — More Complex Logical Tests

## 1. In CASE Things Get More Complex

Now that you understand the basics of `CASE` statements, let's set up some more complex logical tests.

## 2. Reviewing CASE WHEN

Previously, we covered `CASE` statements with one logical test in a `WHEN` statement, returning outcomes based on whether that test is `TRUE` or `FALSE`.

This example tests whether home or away goals were higher and identifies the team with the higher score as the winner.

Everything `ELSE` is categorized as a tie.

The resulting table has one column identifying matches as one of **three possible outcomes**:

- 🏠 Home win
- ✈️ Away win
- 🤝 Tie

### Basic CASE Example

    CASE
        WHEN home_goal > away_goal THEN 'Home win'
        WHEN home_goal < away_goal THEN 'Away win'
        ELSE 'Tie'
    END AS outcome

## 3. CASE WHEN ... AND Then Some

If you want to test **multiple logical conditions** in a `CASE` statement, you can use `AND` inside your `WHEN` clause.

For example, let's see if each match was played and won by the team **Chelsea**.

Each `WHEN` clause contains two logical tests.

The first tests if the `hometeam_id` identifies Chelsea, **AND** then tests if the home team scored higher than the away team.

If both conditions are `TRUE`, the new column output returns:

    'Chelsea home win!'

The opposite set of conditions is included in a second `WHEN` statement.

If the `awayteam_id` belongs to Chelsea **AND** Chelsea scored higher, the output returns:

    'Chelsea away win!'

All other matches are categorized as:

    'Loss or tie :('

### Example

    CASE
        WHEN hometeam_id = 8455 AND home_goal > away_goal
            THEN 'Chelsea home win!'

        WHEN awayteam_id = 8455 AND away_goal > home_goal
            THEN 'Chelsea away win!'

        ELSE 'Loss or tie :('
    END AS outcome

### 🔍 Understanding AND

`AND` requires **both conditions** to be true.

For example:

    hometeam_id = 8455
    AND
    home_goal > away_goal

This means:

1. 🏠 Chelsea must be the home team.
2. ⚽ Chelsea must score more goals than the away team.

Only when **both** are true will SQL return `Chelsea home win!`.

## 4. ⚠️ What ELSE Is Being Excluded?

When testing logical conditions, it's important to carefully consider which rows of your data are part of your `ELSE` clause and whether they're categorized correctly.

Here's the same `CASE` statement from the previous example, but with the `WHERE` filter removed.

Without the filter, your `ELSE` clause will categorize **ALL matches** played by anyone who doesn't meet the first two conditions as:

    'Loss or tie :('

This creates a problem.

A quick look at the results shows that the first few matches are all categorized as `Loss or tie`, but neither the `hometeam_id` nor `awayteam_id` belongs to Chelsea.

### ❌ The Problem

The `ELSE` clause doesn't automatically mean:

> Chelsea lost or tied.

It actually means:

> None of the previous `WHEN` conditions were true.

Therefore, matches involving completely different teams can also fall into the `ELSE` category.

### 🧠 Important Rule

Always ask:

**"Which rows can reach my `ELSE` clause?"**

This is especially important when using `CASE` to analyze a specific team, group, or category.

## 5. ✅ Correctly Categorize Your Data with CASE

The easiest way to correct this is to ensure you add specific filters in the `WHERE` clause that exclude all teams where Chelsea did not play.

Here, we specify this using an `OR` statement in `WHERE`.

We retrieve only results where the Chelsea ID, `8455`, is present in either:

- `hometeam_id`
- `awayteam_id`

### Example

    WHERE hometeam_id = 8455
       OR awayteam_id = 8455

The resulting table clearly specifies whether Chelsea was the **home or away team**.

### 🔍 AND vs OR

These two operators have different purposes:

| Operator | Meaning |
|---|---|
| `AND` | Both conditions must be true |
| `OR` | At least one condition must be true |

For example:

    hometeam_id = 8455
    AND home_goal > away_goal

Means both conditions must be true.

But:

    hometeam_id = 8455
    OR awayteam_id = 8455

Means Chelsea can appear in either position.

## 6. ❓ What's NULL?

It's also important to consider what your `ELSE` clause is doing.

These two queries are identical except for the `ELSE NULL` statement specified in the second.

### Without ELSE

    CASE
        WHEN condition THEN result
    END AS outcome

### With ELSE NULL

    CASE
        WHEN condition THEN result
        ELSE NULL
    END AS outcome

They both return identical results — a table with quite a few `NULL` results.

This happens because when no `WHEN` condition is true, SQL returns `NULL` if there is no `ELSE` clause or if the `ELSE` explicitly returns `NULL`.

### 💡 What Is NULL?

`NULL` represents a **missing or unknown value**.

It is not the same as:

- `0`
- An empty string `''`
- `FALSE`

## 7. 🔎 What Are Your NULL Values Doing?

Let's say we're only interested in viewing the results of games where Chelsea **won**, and we don't care if they lose or tie.

Just like in the previous example, simply removing the `ELSE` clause will still retrieve those results — but it will also produce a lot of `NULL` values.

For example:

    CASE
        WHEN hometeam_id = 8455 AND home_goal > away_goal
            THEN 'Chelsea home win!'

        WHEN awayteam_id = 8455 AND away_goal > home_goal
            THEN 'Chelsea away win!'
    END AS outcome

The matches that don't meet either condition receive `NULL`.

### ⚠️ Important

A `CASE` statement does **not automatically remove rows**.

It creates a value for each row.

If no condition is satisfied and there is no `ELSE`, the resulting value is `NULL`.

## 8. 📍 Where to Place Your CASE?

To correct this, you can treat the **entire `CASE` statement as a column** to filter by in your `WHERE` clause, just like any other column.

In order to filter a query by a `CASE` statement, you include the entire `CASE` statement in the `WHERE` clause.

## 9. 📍 Filtering by a CASE Statement

You include the entire `CASE` statement, **except its alias**, in `WHERE`.

You then specify what you want to include or exclude.

For this query, we want to keep all rows where the `CASE` statement:

    IS NOT NULL

### Example

    SELECT
        date,
        CASE
            WHEN hometeam_id = 8455 AND home_goal > away_goal
                THEN 'Chelsea home win!'

            WHEN awayteam_id = 8455 AND away_goal > home_goal
                THEN 'Chelsea away win!'
        END AS outcome

    FROM matches_spain

    WHERE
        CASE
            WHEN hometeam_id = 8455 AND home_goal > away_goal
                THEN 'Chelsea home win!'

            WHEN awayteam_id = 8455 AND away_goal > home_goal
                THEN 'Chelsea away win!'
        END IS NOT NULL;

The resulting table now only includes **Chelsea's home and away wins**.

We don't need to filter by Chelsea's team ID separately because the `CASE` statement itself determines which rows qualify.

### 🧠 Why Does This Work?

The `CASE` statement produces:

- `Chelsea home win!` → not `NULL` → ✅ Keep
- `Chelsea away win!` → not `NULL` → ✅ Keep
- No matching condition → `NULL` → ❌ Exclude

So:

    CASE ... END IS NOT NULL

acts as a filter for the rows where the `CASE` statement successfully identified a Chelsea win.

## 🔑 CASE + WHERE Pattern

A useful pattern to remember is:

    SELECT
        CASE
            WHEN condition_1 THEN 'Result 1'
            WHEN condition_2 THEN 'Result 2'
        END AS category

    FROM table_name

    WHERE
        CASE
            WHEN condition_1 THEN 'Result 1'
            WHEN condition_2 THEN 'Result 2'
        END IS NOT NULL;

This is useful when you want to:

- 🎯 Identify specific conditions
- 🏷️ Create categories
- 🧹 Exclude rows that don't belong to those categories
- 🚫 Remove unwanted `NULL` results

## 10. 🏋️ Let's Practice!

Okay! Let's practice some more complex `CASE` statements.

# 🧠 Key Takeaways

- `CASE` statements can contain multiple logical conditions.
- Use `AND` when **both conditions must be true**.
- Use `OR` when **at least one condition must be true**.
- `ELSE` catches every row that doesn't satisfy a previous `WHEN` condition.
- Be careful about what rows can reach the `ELSE` clause.
- A `WHERE` filter can restrict the data before or independently of the `CASE` logic.
- Without an `ELSE`, a `CASE` statement returns `NULL` when no condition is met.
- `NULL` represents a missing or unknown value.
- A `CASE` statement can be used directly in a `WHERE` clause.
- `IS NOT NULL` can be used to keep only rows where the `CASE` statement produced a result.
- When analyzing a specific team, make sure your filtering logic prevents unrelated teams from being incorrectly classified.

# 📌 Quick Reference

### Simple CASE

    CASE
        WHEN condition THEN result
        ELSE other_result
    END AS new_column

### Multiple Conditions with AND

    CASE
        WHEN condition_1 AND condition_2 THEN result
        ELSE other_result
    END AS new_column

### Multiple Conditions with OR

    WHERE condition_1
       OR condition_2

### CASE Without ELSE

    CASE
        WHEN condition THEN result
    END AS new_column

### Filter CASE Results

    WHERE
        CASE
            WHEN condition_1 THEN result_1
            WHEN condition_2 THEN result_2
        END IS NOT NULL
