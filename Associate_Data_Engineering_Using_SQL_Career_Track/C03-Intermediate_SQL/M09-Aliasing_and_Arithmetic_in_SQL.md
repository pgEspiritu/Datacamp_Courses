# Aliasing and Arithmetic in SQL ➕➖✖️➗

## Overview 📚

This lesson covers:

- Basic arithmetic in SQL.
- Arithmetic with integers and decimals.
- The difference between **aggregate functions** and arithmetic.
- Using `AS` to create aliases for calculated fields.
- Why aliases cannot generally be used in the `WHERE` clause when defined in `SELECT`.

# 1. Arithmetic in SQL 🧮

SQL supports basic arithmetic operators:

| Operator | Operation | Example |
|---|---|---|
| `+` | Addition | `10 + 5` |
| `-` | Subtraction | `10 - 5` |
| `*` | Multiplication | `10 * 5` |
| `/` | Division | `10 / 5` |

### Examples

`SELECT 10 + 5;`

`SELECT 10 - 5;`

`SELECT 10 * 5;`

`SELECT 10 / 5;`

## Parentheses

Parentheses can be used to make the intended calculation clearer.

Example:

`SELECT (10 + 5) * 2;`

Parentheses indicate which calculation should be performed first.

Even when parentheses are not required, they can improve **readability and clarity**.

# 2. Integer Division ⚠️

SQL can behave differently when dividing integers.

When an integer is divided by another integer, SQL may return an **integer result**, discarding the fractional portion.

Example:

`SELECT 5 / 3;`

may return:

`1`

instead of:

`1.666...`

### Why?

The operands are both integers:

- `5` = integer
- `3` = integer

Therefore, integer division is performed.

## Getting Decimal Precision

Use decimal values when you want a decimal result.

Example:

`SELECT 4.0 / 3.0;`

Result:

`1.333...`

### Key Rule

**Integer ÷ Integer → Integer result**

**Decimal ÷ Decimal → Decimal result**

Therefore, be careful when performing division and make sure the operands use the appropriate numeric type when decimal precision is needed.

# 3. Aggregate Functions vs. Arithmetic 📊

Aggregate functions and arithmetic both perform calculations, but they work differently.

## Aggregate Functions

Aggregate functions operate across **multiple values in a column/field**.

Examples:

- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`
- `COUNT()`

Think of this as calculating **vertically** down a column.

Example:

`SELECT SUM(budget) FROM films;`

This combines values from many rows in the `budget` column.

## Arithmetic

Arithmetic operators perform calculations on values, often **horizontally across fields in the same record**.

Example:

`SELECT gross - budget FROM films;`

For each film, SQL calculates:

**Gross − Budget = Profit**

### Key Difference

**Aggregate functions → Across rows/values in a column**

**Arithmetic → Between values/fields within a record**

# 4. Example: Calculating Profit 💰

Suppose the `films` table contains:

- `gross` = Amount earned by the film
- `budget` = Amount spent to produce the film

We can calculate profit using:

`SELECT gross - budget FROM films;`

The result represents:

**Profit = Gross − Budget**

### Why Alias the Result?

The calculation does not automatically provide a useful field name.

Instead of an unclear result column name, use an alias:

`SELECT gross - budget AS profit FROM films;`

Now the result is clearly labeled:

`profit`

# 5. Aliasing Calculations with AS ✏️

The `AS` keyword creates an **alias** for a calculated expression or field.

Example:

`SELECT gross - budget AS profit FROM films;`

### Meaning

- `gross - budget` → Calculation
- `AS` → Assign an alias
- `profit` → Name shown in the result

### Important

The alias does **not** create a new field in the underlying table.

It only gives the calculated result a readable name in the query output.

# 6. Aliasing Aggregate Functions 📊

Aliases are especially useful with aggregate functions.

Without aliases:

`SELECT MAX(budget), MAX(gross) FROM films;`

The result may contain two columns both labeled:

`max`

This is unclear.

### Better

`SELECT MAX(budget) AS max_budget, MAX(gross) AS max_gross FROM films;`

Now each result has a meaningful name.

### Best Practice

> **Always use clear aliases for calculated or aggregated results.**

This improves:

- Readability
- Interpretation
- Reporting
- Maintainability

# 7. Aliasing Multiple Calculations

You can alias multiple expressions in the same query.

Example:

`SELECT AVG(budget) AS average_budget, MAX(budget) AS maximum_budget, gross - budget AS profit FROM films;`

Each output column has a clear description.

# 8. SQL Execution Order and Aliases 🔄

The simplified SQL execution order covered so far is:

**FROM → WHERE → SELECT → LIMIT**

The alias is created during the **`SELECT`** step.

Therefore, an alias created in `SELECT` is generally **not available to `WHERE`**, because `WHERE` is processed first.

## Example

Suppose we write:

`SELECT gross - budget AS profit FROM films WHERE profit > 1000000;`

This causes an error because:

- `FROM` is processed first.
- `WHERE` is processed next.
- `SELECT` is processed later.
- The alias `profit` does not exist yet when `WHERE` is evaluated.

### Key Concept

**Alias created in SELECT → Too late for WHERE**

# 9. Why Can't WHERE Use the SELECT Alias?

Consider:

`SELECT gross - budget AS profit FROM films WHERE profit > 1000000;`

Logical sequence:

1. `FROM films`
2. `WHERE profit > 1000000`
3. `SELECT gross - budget AS profit`

At the moment SQL evaluates:

`WHERE profit > 1000000`

the alias `profit` has not yet been created.

Therefore, the query fails.

### Important

The issue is caused by the **logical order of SQL processing**, not by the alias itself being invalid.

# 10. Arithmetic and Aliasing Together 🔗

Calculated fields should generally be given meaningful aliases.

Example:

`SELECT gross - budget AS profit FROM films;`

Another example:

`SELECT budget / 1000000.0 AS budget_millions FROM films;`

This makes the meaning of the output immediately clear.

# 11. Practical Examples 🎯

## Add Two Values

`SELECT 10 + 20 AS total;`

## Subtract Values

`SELECT 100 - 40 AS difference;`

## Multiply Values

`SELECT 10 * 5 AS product;`

## Divide Values

`SELECT 10.0 / 4.0 AS result;`

## Calculate Film Profit

`SELECT gross - budget AS profit FROM films;`

## Calculate Maximum Budget

`SELECT MAX(budget) AS maximum_budget FROM films;`

## Calculate Multiple Aggregates

`SELECT AVG(budget) AS average_budget, MAX(budget) AS maximum_budget FROM films;`

# 12. Common Mistakes ⚠️

### Mistake 1: Forgetting Integer Division

`SELECT 5 / 3;`

may return:

`1`

when you expected:

`1.666...`

Use decimal values when decimal precision is required:

`SELECT 5.0 / 3.0;`

### Mistake 2: Not Using an Alias for Calculations

Less clear:

`SELECT gross - budget FROM films;`

Better:

`SELECT gross - budget AS profit FROM films;`

### Mistake 3: Reusing Ambiguous Aggregate Names

Less clear:

`SELECT MAX(budget), MAX(gross) FROM films;`

Better:

`SELECT MAX(budget) AS max_budget, MAX(gross) AS max_gross FROM films;`

### Mistake 4: Using a SELECT Alias in WHERE

❌

`SELECT gross - budget AS profit FROM films WHERE profit > 1000000;`

The alias is created during `SELECT`, but `WHERE` is processed first.

# 13. Aggregate vs. Arithmetic Example 🧠

Suppose the table contains:

| Film | Gross | Budget |
|---|---:|---:|
| A | 100 | 50 |
| B | 200 | 80 |
| C | 300 | 120 |

### Arithmetic

`SELECT gross - budget AS profit FROM films;`

Results:

- Film A → `50`
- Film B → `120`
- Film C → `180`

The calculation happens **for each record**.

### Aggregate

`SELECT SUM(gross) FROM films;`

Result:

`600`

The aggregate operates across the column's values.

### Summary

**Arithmetic → Record-level calculation**

**Aggregate → Dataset/subset-level calculation**

# Exam / Interview Key Points 🎯

- SQL supports `+`, `-`, `*`, and `/`.
- Parentheses can clarify the intended order of arithmetic operations.
- Integer division can return an integer instead of a decimal.
- Use decimal operands when you need fractional precision.
- Aggregate functions operate across multiple values in a column.
- Arithmetic commonly performs calculations between fields within individual records.
- `SUM()`, `AVG()`, `MIN()`, `MAX()`, and `COUNT()` are aggregate functions.
- `AS` creates an alias for a field or calculated result.
- Aliases improve readability and make calculated or summarized results easier to understand.
- Aliases do not rename the underlying database field.
- Calculated expressions should generally be given meaningful aliases.
- Multiple aggregate functions can produce ambiguous output names such as multiple `max` columns, so aliases are important.
- The simplified logical execution order is:
  - **FROM → WHERE → SELECT → LIMIT**
- A `SELECT` alias generally cannot be referenced in `WHERE` because `WHERE` is processed before `SELECT`.
- Example:
  - `gross - budget AS profit`
  - `profit` is created during `SELECT`.
  - `WHERE` cannot use that alias during its earlier processing step.

# Quick Memory Aid 🚀

**`+` = Add**

**`-` = Subtract**

**`*` = Multiply**

**`/` = Divide**

**Integer ÷ Integer → Integer result**

**Decimal ÷ Decimal → Decimal result**

**Aggregate = Across rows/column**

**Arithmetic = Between fields/values in a record**

**AS = Rename the output**

**FROM → WHERE → SELECT → LIMIT**

### Most Important Alias Rule

> **If an alias is created in `SELECT`, don't expect to use it in `WHERE`, because `WHERE` is logically processed before `SELECT`.**

# Core Concept ⭐

> **SQL arithmetic performs calculations using operators such as `+`, `-`, `*`, and `/`, while aggregate functions summarize values across multiple records. Use `AS` to give calculated and aggregated results meaningful names, and remember that aliases created in `SELECT` are not available to `WHERE` because `WHERE` is processed first.**
