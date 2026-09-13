# Filtering Text in SQL 🔍

## Overview 📚

The `WHERE` clause can be used to filter **textual data**.

Previously, filtering text required an exact match, such as:

`WHERE country = 'Japan'`

In real-world data, we often need to search for **patterns** rather than exact text.

SQL provides three useful operators for this:

- `LIKE`
- `NOT LIKE`
- `IN`

# 1. LIKE 🔎

The `LIKE` operator is used with `WHERE` to search for a **pattern** in a text field.

Example:

`SELECT name FROM people WHERE name LIKE 'Ad%';`

This searches for names beginning with `Ad`.

## LIKE Wildcards

`LIKE` uses two main wildcard characters:

| Wildcard | Meaning |
|---|---|
| `%` | Matches zero, one, or many characters |
| `_` | Matches exactly one character |

# 2. Percent Wildcard `%`

The `%` wildcard represents **zero, one, or many characters**.

Example:

`WHERE name LIKE 'Ad%'`

This can match:

- Adel
- Adelaide
- Aden

because the characters after `Ad` can be anything, including nothing.

## Percent Wildcard Positions

The `%` wildcard can appear anywhere.

### Starts With

`WHERE name LIKE 'Ad%'`

Matches values that **start with `Ad`**.

### Ends With

`WHERE name LIKE '%r'`

Matches values that **end with `r`**.

### Contains

`WHERE name LIKE '%data%'`

Matches values that **contain `data` anywhere** in the text.

### Before and After a Pattern

`WHERE name LIKE '%ad%'`

Matches values where `ad` occurs anywhere in the string.

# 3. Underscore Wildcard `_`

The `_` wildcard represents **exactly one character**.

Example:

`WHERE name LIKE '___'`

Matches values containing exactly **three characters**.

For example:

- Eve ✅
- Eva ✅
- John ❌

## Specific Character Position

Underscores can be combined with other characters.

Example:

`WHERE name LIKE '__t%'`

This means:

- First character → anything
- Second character → anything
- Third character → `t`
- Remaining characters → anything

Therefore, it finds records where the **third character is `t`**.

# 4. Combining Wildcards 🧩

`%` and `_` can be used together.

Example:

`WHERE name LIKE '_a%'`

Meaning:

- First character → any single character
- Second character → `a`
- Remaining characters → zero or more characters

This allows very flexible pattern matching.

# 5. NOT LIKE 🚫

`NOT LIKE` finds records that **do not match a specified text pattern**.

Example:

`SELECT * FROM people WHERE name NOT LIKE 'A.%';`

This returns records whose names do not match the specified pattern.

> **LIKE = Match the pattern**

> **NOT LIKE = Do not match the pattern**

## Important: Case Sensitivity ⚠️

The lesson notes that `LIKE` and `NOT LIKE` are **case-sensitive**, so the capitalization of the search pattern matters.

For example:

`WHERE name LIKE 'A%'`

may behave differently from:

`WHERE name LIKE 'a%'`

depending on the database and configuration.

Therefore, pay attention to the case used in the search criteria.

# 6. Wildcard Position 📍

Wildcards can be placed in different positions depending on the pattern you want.

| Goal | Example |
|---|---|
| **Starts with** | `LIKE 'Ad%'` |
| **Ends with** | `LIKE '%r'` |
| **Contains** | `LIKE '%ad%'` |
| **Exactly 3 characters** | `LIKE '___'` |
| **Third character is `t`** | `LIKE '__t%'` |

### Quick Memory Aid

`%` = **Any number of characters**

`_` = **Exactly one character**

# 7. IN 🔢

When filtering based on multiple specific values, you could use several `OR` conditions.

For example:

`WHERE release_year = 1920 OR release_year = 1930 OR release_year = 1940`

This works, but can become difficult to read.

The `IN` operator provides a shorter and cleaner alternative.

Example:

`WHERE release_year IN (1920, 1930, 1940)`

### Meaning

`IN` means:

> Match any value in the specified list.

## OR vs. IN

These two conditions are equivalent:

`WHERE release_year = 1920 OR release_year = 1930 OR release_year = 1940`

`WHERE release_year IN (1920, 1930, 1940)`

### Advantage of IN

`IN` is:

- More concise.
- Easier to read.
- Easier to maintain.
- Cleaner than chaining many `OR` conditions.

# 8. IN with Text 🔤

`IN` can also be used with strings.

Example:

`SELECT title FROM films WHERE country IN ('Germany', 'France');`

This returns films where the country is either:

- Germany
- France

### Important

String values inside an `IN` list use **single quotation marks**.

Numbers do not require quotation marks.

Correct:

`WHERE release_year IN (1920, 1930, 1940)`

Correct:

`WHERE country IN ('Germany', 'France')`

# 9. LIKE vs. IN

These operators serve different purposes.

| Operator | Purpose | Example |
|---|---|---|
| `LIKE` | Search for a text pattern | `name LIKE 'Ad%'` |
| `NOT LIKE` | Exclude a text pattern | `name NOT LIKE 'Ad%'` |
| `IN` | Match one of several specific values | `country IN ('Germany', 'France')` |

### Key Difference

**LIKE = Pattern matching**

**IN = Exact matching against a list of values**

For example:

`LIKE 'Ger%'`

means:

> Text beginning with `Ger`.

Whereas:

`IN ('Germany', 'France')`

means:

> Exactly Germany or exactly France.

# 10. Practical Examples 🎯

## Names Starting with "A"

`SELECT name FROM people WHERE name LIKE 'A%';`

## Names Ending with "r"

`SELECT name FROM people WHERE name LIKE '%r';`

## Names Containing "an"

`SELECT name FROM people WHERE name LIKE '%an%';`

## Exactly Three Characters

`SELECT name FROM people WHERE name LIKE '___';`

## Third Character Is "t"

`SELECT name FROM people WHERE name LIKE '__t%';`

## Exclude Names Matching a Pattern

`SELECT name FROM people WHERE name NOT LIKE 'A%';`

## Films from 1920, 1930, or 1940

`SELECT title FROM films WHERE release_year IN (1920, 1930, 1940);`

## Films from Germany or France

`SELECT title FROM films WHERE country IN ('Germany', 'France');`

# 11. Combining WHERE with Text Filtering 🔗

These operators are used together with `WHERE`.

### Pattern Matching

`WHERE name LIKE 'Ad%'`

### Pattern Exclusion

`WHERE name NOT LIKE 'Ad%'`

### Multiple Exact Values

`WHERE country IN ('Germany', 'France')`

# 12. Common Mistakes ⚠️

### Mistake 1: Forgetting Quotes Around Strings

❌

`WHERE country IN (Germany, France)`

✅

`WHERE country IN ('Germany', 'France')`

### Mistake 2: Using `=` When a Pattern Is Needed

❌

`WHERE name = 'Ad%'`

✅

`WHERE name LIKE 'Ad%'`

`=` checks for an exact value, while `LIKE` performs pattern matching.

### Mistake 3: Confusing `%` and `_`

`%` = zero, one, or many characters

`_` = exactly one character

### Mistake 4: Incorrect IN Syntax

❌

`WHERE country IN 'Germany', 'France'`

✅

`WHERE country IN ('Germany', 'France')`

The values must be enclosed in parentheses.

# Exam / Interview Key Points 🎯

- `LIKE` is used with `WHERE` for **pattern matching**.
- `NOT LIKE` returns records that **do not match a pattern**.
- `%` matches **zero, one, or many characters**.
- `_` matches **exactly one character**.
- Wildcards can be placed anywhere within a pattern.
- `%` at the beginning allows text to appear before the searched pattern.
- `%` at the end allows text to appear after the searched pattern.
- `LIKE 'Ad%'` finds values starting with `Ad`.
- `LIKE '%r'` finds values ending with `r`.
- `LIKE '%ad%'` finds values containing `ad`.
- `LIKE '___'` matches values with exactly three characters.
- `LIKE '__t%'` matches values where the third character is `t`.
- The lesson notes that `LIKE` and `NOT LIKE` are **case-sensitive**.
- `IN` allows multiple specific values to be included in a `WHERE` condition.
- `IN` is a cleaner alternative to chaining multiple `OR` conditions.
- `IN` can be used with both numbers and strings.
- String values in an `IN` list use **single quotes**.
- `LIKE` performs **pattern matching**.
- `IN` performs **exact matching against a list of values**.

# Quick Memory Aid 🚀

**LIKE = Pattern**

**NOT LIKE = Exclude Pattern**

**IN = One of these exact values**

**`%` = 0 or more characters**

**`_` = Exactly 1 character**

### Pattern Examples

`'Ad%'` → Starts with `Ad`

`'%r'` → Ends with `r`

`'%ad%'` → Contains `ad`

`'___'` → Exactly 3 characters

`'__t%'` → Third character is `t`

### IN Example

`IN ('Germany', 'France')` → Germany OR France

# Most Important Concept ⭐

> **Use `LIKE` and `NOT LIKE` when you need to match or exclude text patterns, using `%` for zero or more characters and `_` for exactly one character. Use `IN` when you need to match a field against multiple specific values, providing a cleaner alternative to multiple `OR` conditions.**
