# Multiple Criteria in SQL 🔍

## Overview 📚

Sometimes a query needs to filter data using **more than one condition**.

SQL provides several operators and keywords for combining filtering criteria:

- `OR`
- `AND`
- `BETWEEN`

These allow us to create more specific and powerful `WHERE` conditions.

# 1. OR Operator 🔀

`OR` is used when **at least one condition must be true**.

### Meaning

**OR = This condition OR that condition**

Example:

`SELECT title FROM films WHERE release_year = 1994 OR release_year = 2000;`

This returns films released in:

- 1994
- 2000

### Important Rule ⚠️

When using `OR`, specify the **field and condition for every condition**.

✅ Correct:

`WHERE release_year = 1994 OR release_year = 2000`

❌ Incorrect:

`WHERE release_year = 1994 OR 2000`

The second condition must specify what `2000` is being compared to.

### Quick Memory Aid

**OR = At least one condition is true**

# 2. AND Operator 🤝

`AND` is used when **all specified conditions must be true**.

Example:

`SELECT title FROM films WHERE release_year >= 1994 AND release_year <= 2000;`

This returns films released from 1994 through 2000.

### Important Rule

As with `OR`, the field and operator should be specified for **each condition**.

✅ Correct:

`WHERE release_year >= 1994 AND release_year <= 2000`

### Quick Memory Aid

**AND = All conditions must be true**

# 3. OR vs. AND 🧠

| Operator | Meaning | Example |
|---|---|---|
| `OR` | At least one condition must be true | `year = 1994 OR year = 2000` |
| `AND` | All conditions must be true | `year >= 1994 AND year <= 2000` |

## Coat Analogy 🧥

### OR

**Yellow OR short**

A coat qualifies if it is:

- Yellow
- Short
- Or both

### AND

**Yellow AND short**

A coat must be:

- Yellow
- AND short

# 4. Combining AND and OR 🔗

SQL allows `AND` and `OR` to be used together.

Example requirement:

> Films released in **1994 OR 1995**, AND certified **PG OR R**.

Conceptually:

`(release_year = 1994 OR release_year = 1995) AND (certification = 'PG' OR certification = 'R')`

### Why Parentheses Matter

When multiple `AND` and `OR` conditions appear together, use **parentheses** to make the intended logic explicit.

Example:

`WHERE (release_year = 1994 OR release_year = 1995) AND (certification = 'PG' OR certification = 'R')`

This ensures SQL evaluates the conditions in the intended logical groups.

### Logical Structure

**(Condition A OR Condition B) AND (Condition C OR Condition D)**

Meaning:

- Year must be 1994 or 1995.
- Certification must be PG or R.

### Quick Memory Aid

**Parentheses = Control logical grouping**

# 5. BETWEEN 🔢

`BETWEEN` is a shorthand for filtering values within a range.

Instead of:

`WHERE release_year >= 1994 AND release_year <= 2000`

you can write:

`WHERE release_year BETWEEN 1994 AND 2000`

### Meaning

**BETWEEN = Within a specified range**

### Important: BETWEEN Is Inclusive ✅

`BETWEEN` includes both the **starting value and ending value**.

Therefore:

`BETWEEN 1994 AND 2000`

includes:

- 1994 ✅
- 1995 ✅
- ...
- 2000 ✅

### Equivalent Conditions

These two filters are equivalent:

`WHERE release_year >= 1994 AND release_year <= 2000`

`WHERE release_year BETWEEN 1994 AND 2000`

# 6. BETWEEN with AND

The syntax is:

`BETWEEN start_value AND end_value`

Example:

`SELECT title FROM films WHERE release_year BETWEEN 1994 AND 2000;`

This returns all films released from **1994 through 2000, inclusive**.

### Important Distinction

`BETWEEN` itself uses the keyword `AND`:

`BETWEEN 1994 AND 2000`

This is different from using `AND` to create two separate conditions.

# 7. BETWEEN with Multiple Conditions 🔗

`BETWEEN` can be combined with other filtering operators.

Example:

`SELECT title FROM films WHERE release_year BETWEEN 1994 AND 2000 AND country = 'United Kingdom';`

This returns films:

- Released between 1994 and 2000.
- From the United Kingdom.

### Logical Structure

**Release year in range AND country = United Kingdom**

# 8. Combining BETWEEN, AND, and OR 🚀

SQL allows increasingly complex filters by combining these operators.

Example:

`WHERE release_year BETWEEN 1994 AND 2000 AND (country = 'United Kingdom' OR country = 'Japan')`

This means:

- Film must be released between 1994 and 2000.
- Country must be either United Kingdom or Japan.

## Complex Filtering Structure

`WHERE (Condition A OR Condition B) AND (Condition C OR Condition D)`

or:

`WHERE Condition A AND Condition B AND (Condition C OR Condition D)`

Parentheses make the intended logic clear and prevent unexpected results.

# 9. Practical Examples 🎯

## Films from 1994 or 2000

`SELECT title FROM films WHERE release_year = 1994 OR release_year = 2000;`

## Films from 1994 through 2000

`SELECT title FROM films WHERE release_year >= 1994 AND release_year <= 2000;`

## Same Range Using BETWEEN

`SELECT title FROM films WHERE release_year BETWEEN 1994 AND 2000;`

## Films from 1994 or 1995 with PG or R Certification

`SELECT title FROM films WHERE (release_year = 1994 OR release_year = 1995) AND (certification = 'PG' OR certification = 'R');`

## Films from 1994–2000 from the United Kingdom

`SELECT title FROM films WHERE release_year BETWEEN 1994 AND 2000 AND country = 'United Kingdom';`

# 10. Logical Interpretation 🧩

## OR

`A OR B`

Possible outcomes:

| A | B | Result |
|---|---|---|
| TRUE | TRUE | TRUE |
| TRUE | FALSE | TRUE |
| FALSE | TRUE | TRUE |
| FALSE | FALSE | FALSE |

**At least one must be TRUE.**

## AND

`A AND B`

Possible outcomes:

| A | B | Result |
|---|---|---|
| TRUE | TRUE | TRUE |
| TRUE | FALSE | FALSE |
| FALSE | TRUE | FALSE |
| FALSE | FALSE | FALSE |

**Both must be TRUE.**

# 11. Common Mistakes ⚠️

### Mistake 1: Incomplete OR Condition

❌

`WHERE release_year = 1994 OR 2000`

✅

`WHERE release_year = 1994 OR release_year = 2000`

### Mistake 2: Incomplete AND Condition

❌

`WHERE release_year >= 1994 AND <= 2000`

✅

`WHERE release_year >= 1994 AND release_year <= 2000`

### Mistake 3: Missing Parentheses

When mixing `AND` and `OR`, failing to group conditions can produce results different from what you intended.

Better:

`WHERE (release_year = 1994 OR release_year = 1995) AND (certification = 'PG' OR certification = 'R')`

### Mistake 4: Forgetting BETWEEN Is Inclusive

`BETWEEN 1994 AND 2000`

includes both:

- 1994
- 2000

# 12. Operator Comparison 📊

| Keyword | Purpose | Example |
|---|---|---|
| `OR` | At least one condition must be true | `country = 'UK' OR country = 'USA'` |
| `AND` | All conditions must be true | `year >= 1994 AND year <= 2000` |
| `BETWEEN` | Filter within a range | `year BETWEEN 1994 AND 2000` |

# Exam / Interview Key Points 🎯

- `OR` allows a record to satisfy **at least one** condition.
- `AND` requires **all conditions** to be true.
- Every `OR` or `AND` condition should specify the relevant field and comparison.
- `BETWEEN` is shorthand for filtering a value within a range.
- `BETWEEN` is **inclusive** of both the start and end values.
- `BETWEEN 1994 AND 2000` includes **1994 and 2000**.
- `BETWEEN` can replace:
  - `>= start`
  - `AND <= end`
- `AND` and `OR` can be combined in a single `WHERE` clause.
- Use **parentheses** when combining `AND` and `OR` to explicitly control logical grouping.
- Parentheses help prevent unexpected filtering results.
- Complex filters can combine:
  - `WHERE`
  - `AND`
  - `OR`
  - `BETWEEN`

# Quick Memory Aid 🚀

**OR = Any one**

**AND = All**

**BETWEEN = Range**

**BETWEEN = Inclusive ✅**

**AND + OR = Use parentheses when grouping is important**

### Easy Rules

> **OR → At least one condition**

> **AND → Every condition**

> **BETWEEN → Start and end are included**

> **Multiple AND/OR conditions → Group with parentheses**

# Most Important Concept ⭐

> **Use `OR` when at least one condition should be true, `AND` when all conditions must be true, and `BETWEEN` as a shorthand for an inclusive range. When combining `AND` and `OR`, use parentheses to clearly define the intended logical groups.**
