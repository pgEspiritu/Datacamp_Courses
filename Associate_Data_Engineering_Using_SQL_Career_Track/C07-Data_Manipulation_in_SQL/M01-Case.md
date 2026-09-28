# Intermediate SQL

## 1. Welcome to Intermediate SQL!

Hello, and welcome to Intermediate SQL. My name is Mona Khalil. I am a Curriculum Lead with DataCamp, and I will be your instructor for this course. SQL is a powerful tool for working with relational databases. With an intermediate knowledge of SQL, you will gain the ability to access and create robust data sets from multiple tables in a relational database to answer your data science questions.

## 2. Topics Covered

In this course, you will specifically learn how to shape, transform, and manipulate data using:

- `CASE` statements
- Simple subqueries
- Correlated subqueries
- Window functions

## 3. Prerequisites

Before taking this course, you should be comfortable working with introductory SQL topics, such as selecting data from a database using arithmetic functions, `GROUP BY` statements, and `WHERE` clauses to filter data.

In short, the query on top should look pretty familiar to you.

You should also be familiar with joining data with:

- `LEFT JOIN`
- `RIGHT JOIN`
- `INNER JOIN`
- `OUTER JOIN`

In this course, we will use and build upon these topics to interact with our database.

Alright, let's get started!

## 4. Selecting from the European Soccer Database

For this course, we will be using the **European Soccer Database** — a relational database that contains data about over 25,000 matches, 300 teams, and 10,000 players in Europe between 2008 and 2016.

The data is contained within four tables:

- `country`
- `league`
- `team`
- `match`

Selecting from tables in this database is pretty simple.

The query shown in the lesson gives you the number of matches played in each of the 11 leagues listed in the `league` table.

## 5. Selecting from the European Soccer Database

Let's say we want to compare the number of home team wins, away team wins, and ties in the 2013/2014 season.

The `match` table has two relevant columns:

- `home_goal`
- `away_goal`

## 6. Selecting from the European Soccer Database

We can potentially add filters to the `WHERE` clause, selecting wins, losses, and ties as separate queries.

However, that's not very efficient if you want to compare these separate outcomes in a single data set.

This is where the `CASE` statement comes in.

## 7. CASE Statements

`CASE` statements are SQL's version of an **"IF this THEN that"** statement.

`CASE` statements have three parts:

1. A `WHEN` clause
2. A `THEN` clause
3. An `ELSE` clause

The first part — the `WHEN` clause — tests a given condition, such as:

    WHEN x = 1

If this condition is `TRUE`, it returns the item you specify after your `THEN` clause.

You can create multiple conditions by listing `WHEN` and `THEN` statements within the same `CASE` statement.

For example:

    CASE
        WHEN condition_1 THEN result_1
        WHEN condition_2 THEN result_2
        WHEN condition_3 THEN result_3
        ELSE result_other
    END

The `ELSE` clause returns a specified value if all of your `WHEN` statements are not true.

When you have completed your statement, be sure to include the term `END` and give it an alias.

For example:

    CASE
        WHEN condition_1 THEN result_1
        WHEN condition_2 THEN result_2
        ELSE result_other
    END AS category

The completed `CASE` statement will evaluate to one column in your SQL query.

### Basic CASE Structure

    SELECT
        column_name,
        CASE
            WHEN condition_1 THEN result_1
            WHEN condition_2 THEN result_2
            ELSE result_other
        END AS new_column
    FROM table_name;

## 8. CASE WHEN

In this example, we use a `CASE` statement to create a new variable that identifies matches as:

- Home team wins
- Away team wins
- Ties

A new column is created with the appropriate text for each match given the outcome.

Conceptually, the query looks like this:

    SELECT
        home_goal,
        away_goal,
        CASE
            WHEN home_goal > away_goal THEN 'Home team win'
            WHEN home_goal < away_goal THEN 'Away team win'
            ELSE 'Tie'
        END AS match_outcome
    FROM match;

### How the CASE Statement Works

| Condition | Result |
|---|---|
| `home_goal > away_goal` | Home team win |
| `home_goal < away_goal` | Away team win |
| Otherwise | Tie |

The `CASE` statement allows us to transform numerical values into meaningful categories.

## 9. Let's Practice!

In the next lesson, we will practice more ways of structuring `CASE` statements using arithmetic functions such as:

- `COUNT`
- `SUM`
- `AVG`

For now, you will practice creating `CASE` statements to build categories for your data.

# Key Takeaways

- SQL can be used to work with and manipulate relational databases.
- Intermediate SQL builds upon basic querying, filtering, aggregation, and joins.
- The `CASE` statement works like an `IF...THEN...ELSE` structure.
- A `CASE` statement uses `WHEN`, `THEN`, and `ELSE`.
- A `CASE` statement must end with `END`.
- Use an alias with `AS` to name the resulting column.
- Multiple `WHEN`/`THEN` conditions can be included in one `CASE` statement.
- `CASE` is useful for creating categories from existing data.
- `CASE` can be combined with aggregate functions such as `COUNT`, `SUM`, and `AVG`.
