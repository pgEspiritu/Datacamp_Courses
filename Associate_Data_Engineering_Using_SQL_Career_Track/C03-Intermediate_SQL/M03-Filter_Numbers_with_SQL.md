# Filtering Numbers with SQL 🔍

## Overview 📚

**Filtering** allows us to retrieve only the data relevant to a specific question.

The SQL `WHERE` clause is used to filter records based on a condition.

> **WHERE = Filter the records**

# 1. WHERE Clause

The `WHERE` clause specifies which records should be included in the result.

### Basic Syntax

`SELECT column FROM table WHERE condition;`

Example:

`SELECT title FROM films WHERE release_year > 1960;`

This returns films released **after 1960**.

## Coat Analogy 🧥

Think of a database as a closet full of coats.

- `FROM` → Go to the closet.
- `WHERE` → Find coats matching a condition.
- `SELECT` → Choose what information to retrieve.

Example:

**FROM closet → WHERE color = green → SELECT coat**

# 2. WHERE with Comparison Operators 🔢

Comparison operators allow you to compare numeric values.

| Operator | Meaning | Example |
|---|---|---|
| `>` | Greater than | `release_year > 1960` |
| `<` | Less than | `release_year < 1960` |
| `=` | Equal to | `release_year = 1960` |
| `>=` | Greater than or equal to | `release_year >= 1960` |
| `<=` | Less than or equal to | `release_year <= 1960` |
| `<>` | Not equal to | `release_year <> 1960` |

## Greater Than `>`

Used to find values greater than a specified number.

Example:

`SELECT title FROM films WHERE release_year > 1960;`

Meaning:

> Find films released **after 1960**.

## Less Than `<`

Used to find values smaller than a specified number.

Example:

`SELECT title FROM films WHERE release_year < 1960;`

Meaning:

> Find films released **before 1960**.

## Greater Than or Equal To `>=`

Used to include the specified value and values greater than it.

Example:

`SELECT title FROM films WHERE release_year >= 1960;`

Meaning:

> Find films released **during or after 1960**.

## Less Than or Equal To `<=`

Used to include the specified value and values smaller than it.

Example:

`SELECT title FROM films WHERE release_year <= 1960;`

Meaning:

> Find films released **during or before 1960**.

## Equal To `=`

Used to find an exact matching value.

Example:

`SELECT title FROM films WHERE release_year = 1960;`

Meaning:

> Find films released **in 1960**.

## Not Equal To `<>`

The SQL standard symbol for **not equal to** is:

`<>`

Example:

`SELECT title FROM films WHERE release_year <> 1960;`

Meaning:

> Find films released in **any year except 1960**.

### Important

`<>` means:

**Not equal to**

# 3. WHERE with Strings 🔤

`WHERE` can also be used with text/string values.

When comparing strings, place the string inside **single quotation marks**.

Example:

`SELECT title FROM films WHERE country = 'Japan';`

This returns films where the `country` field is exactly:

`Japan`

### Important Rule

**Numbers → No quotation marks**

Example:

`release_year = 1960`

**Strings → Single quotation marks**

Example:

`country = 'Japan'`

# 4. Numeric vs. String Filtering

| Type | Example | Quotation Marks? |
|---|---|---|
| Number | `release_year = 1960` | ❌ No |
| String | `country = 'Japan'` | ✅ Single quotes |

# 5. WHERE and LIMIT

`WHERE` can be combined with `LIMIT`.

### Written Order

When a query contains all four clauses:

`SELECT`

`FROM`

`WHERE`

`LIMIT`

Example:

`SELECT title FROM films WHERE release_year > 1960 LIMIT 5;`

### Logical Execution Order

The simplified execution order is:

**FROM → WHERE → SELECT → LIMIT**

### Why?

SQL first:

1. Identifies the source table using `FROM`.
2. Filters records using `WHERE`.
3. Selects the requested fields using `SELECT`.
4. Limits the number of returned records using `LIMIT`.

## Example

`SELECT title FROM films WHERE release_year > 1960 LIMIT 5;`

Think of it as:

**FROM films → WHERE release_year > 1960 → SELECT title → LIMIT 5**

This means:

> Find films in the `films` table, keep only films released after 1960, return their titles, and show only the first 5 results.

# 6. Comparison Operators and Their Meanings 🧠

### `>`

**Greater than**

`release_year > 1960`

→ After 1960

### `<`

**Less than**

`release_year < 1960`

→ Before 1960

### `=`

**Equal to**

`release_year = 1960`

→ Exactly 1960

### `>=`

**Greater than or equal to**

`release_year >= 1960`

→ 1960 or later

### `<=`

**Less than or equal to**

`release_year <= 1960`

→ 1960 or earlier

### `<>`

**Not equal to**

`release_year <> 1960`

→ Any year except 1960

# 7. Practical Examples 🎯

## Films After 2000

`SELECT title FROM films WHERE release_year > 2000;`

## Films Before 2000

`SELECT title FROM films WHERE release_year < 2000;`

## Films Released in 2000

`SELECT title FROM films WHERE release_year = 2000;`

## Films Released in or After 2000

`SELECT title FROM films WHERE release_year >= 2000;`

## Films Released in or Before 2000

`SELECT title FROM films WHERE release_year <= 2000;`

## Films Not Released in 2000

`SELECT title FROM films WHERE release_year <> 2000;`

## Films from Japan

`SELECT title FROM films WHERE country = 'Japan';`

## First Five Japanese Films

`SELECT title FROM films WHERE country = 'Japan' LIMIT 5;`

# 8. Common Mistakes ⚠️

### Mistake 1: Using Quotes Around Numbers

❌

`WHERE release_year = '1960'`

✅

`WHERE release_year = 1960`

### Mistake 2: No Quotes Around Strings

❌

`WHERE country = Japan`

✅

`WHERE country = 'Japan'`

### Mistake 3: Using `=` for Not Equal

❌

`WHERE release_year = 1960`

This means **equal to**, not not-equal.

✅

`WHERE release_year <> 1960`

### Mistake 4: Incorrect Clause Order

Correct written order:

`SELECT ... FROM ... WHERE ... LIMIT ...;`

# Exam / Interview Key Points 🎯

- `WHERE` is used to **filter records**.
- `WHERE` focuses the query on records relevant to a specific condition.
- Comparison operators can be used with `WHERE`.
- `>` = greater than.
- `<` = less than.
- `=` = equal to.
- `>=` = greater than or equal to.
- `<=` = less than or equal to.
- `<>` = not equal to.
- `>` can represent values **after** a year.
- `<` can represent values **before** a year.
- Strings must generally be enclosed in **single quotation marks**.
- Numeric values do not need quotation marks.
- When using `SELECT`, `FROM`, `WHERE`, and `LIMIT`, the written order is:

`SELECT → FROM → WHERE → LIMIT`

- The simplified logical execution order is:

`FROM → WHERE → SELECT → LIMIT`

- `WHERE` filters the rows before `SELECT` returns the requested fields.
- `LIMIT` restricts the number of rows returned after filtering.

# Quick Memory Aid 🚀

**WHERE = Which rows?**

**`>` = More than / After**

**`<` = Less than / Before**

**`=` = Exactly**

**`>=` = At least**

**`<=` = At most**

**`<>` = Not equal**

**Number → No quotes**

**String → `'Single quotes'`**

**Execution: FROM → WHERE → SELECT → LIMIT**

# Core Concept ⭐

> **The `WHERE` clause filters records according to a condition. Comparison operators such as `>`, `<`, `=`, `>=`, `<=`, and `<>` allow numeric values to be filtered, while strings should be enclosed in single quotation marks. When combined with `SELECT`, `FROM`, and `LIMIT`, the simplified logical execution order is `FROM → WHERE → SELECT → LIMIT`.**
