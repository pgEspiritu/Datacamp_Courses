# Introducing SQL Queries

## Overview

**SQL queries** are used to retrieve and analyze data from databases.

SQL is especially useful for answering questions:

- Within a single table.
- Across multiple related tables.
- About trends and patterns in large datasets.

## What Is SQL Useful For?

SQL can be used to answer business and analytical questions.

### Library Example

Find out:

> Which books did James check out in 2022?

### HR Example

Query employee salaries in:

- Marketing
- Accounting

to determine whether compensation is comparable across departments.

### Business Examples

SQL can help answer questions such as:

- Which products had the highest sales last week?
- Which products receive the worst customer reviews?
- How did website traffic change after a new feature was introduced?
- What trends are visible in customer reviews?
- What patterns exist in product sales?

## SQL and Other Tools

SQL is often used alongside other tools, such as **spreadsheet applications**.

A common workflow is:

**Database → SQL Query → Results → Spreadsheet / Analysis Tool**

SQL is particularly useful for working with **large datasets** because it can retrieve and analyze large amounts of data efficiently.

# SQL Keywords

**Keywords** are reserved words in SQL that indicate the operation the query should perform.

Two of the most common SQL keywords are:

- `SELECT`
- `FROM`

## SELECT

`SELECT` specifies **which fields/columns you want to retrieve**.

Example:

`SELECT name`

This means:

> Retrieve the `name` field.

## FROM

`FROM` specifies **which table contains the fields being retrieved**.

Example:

`FROM patrons`

This means:

> Get the data from the `patrons` table.

# First SQL Query

To retrieve all patron names:

`SELECT name FROM patrons;`

### Query Structure

**SELECT → What data?**

**FROM → Which table?**

### Important Syntax Rules

- `SELECT` and `FROM` are SQL keywords.
- Keywords are commonly written in **uppercase** for readability.
- Table and field names are kept in **lowercase** in this course.
- A semicolon `;` indicates the end of the query.

## Result Set

The output returned by a SQL query is commonly called a **result set**.

For:

`SELECT name FROM patrons;`

the result set contains the names of all patrons.

# Selecting Multiple Fields

Multiple fields can be selected by listing them after `SELECT` and separating them with commas.

Example:

`SELECT card_num, name FROM patrons;`

This returns:

- `card_num`
- `name`

The fields appear in the **same order** in which they are listed in the query.

### Three Fields

Example:

`SELECT name, card_num, total_fine FROM patrons;`

This returns:

1. `name`
2. `card_num`
3. `total_fine`

## Selecting All Fields

Instead of manually listing every field, SQL provides the **asterisk `*`**, also called a **star** or **wildcard character**.

Example:

`SELECT * FROM patrons;`

This means:

> Select **all fields** from the `patrons` table.

### Comparison

Instead of:

`SELECT card_num, name, year_joined, total_fine FROM patrons;`

you can use:

`SELECT * FROM patrons;`

## Basic SQL Query Pattern

**Select specific fields:**

`SELECT field1, field2 FROM table_name;`

**Select all fields:**

`SELECT * FROM table_name;`

# Query Components

| Component | Purpose |
|---|---|
| `SELECT` | Specifies the fields/columns to retrieve |
| `FROM` | Specifies the table to retrieve data from |
| `,` | Separates multiple fields |
| `*` | Selects all fields |
| `;` | Indicates the end of the query |
| Result set | Output returned by the query |

# Example Queries

### One Field

`SELECT name FROM patrons;`

Returns all patron names.

### Two Fields

`SELECT card_num, name FROM patrons;`

Returns card numbers and names.

### Three Fields

`SELECT name, card_num, total_fine FROM patrons;`

Returns names, card numbers, and fines.

### All Fields

`SELECT * FROM patrons;`

Returns every field in the `patrons` table.

# Exam / Interview Key Points

- **SQL queries** are used to retrieve and analyze database information.
- SQL can answer questions within a table and across related tables.
- SQL is useful for analyzing **large datasets**.
- SQL is often used alongside tools such as spreadsheets.
- **Keywords** are reserved SQL words that indicate operations.
- `SELECT` specifies the fields to retrieve.
- `FROM` specifies the table containing those fields.
- A basic query follows the pattern:
  - `SELECT ... FROM ...;`
- A **semicolon `;`** marks the end of a query.
- A query's output is called a **result set**.
- Multiple fields are separated by **commas**.
- The order of fields after `SELECT` determines their order in the result set.
- `*` means **all fields/columns**.
- `*` is also called a **star** or **wildcard character**.
- SQL keywords are commonly written in uppercase for readability.
- Table and field names are commonly written in lowercase.

# Quick Memory Aid

**SELECT = What do I want?**

**FROM = Where is it?**

**`*` = Everything**

**`,` = Multiple fields**

**`;` = End of query**

**Result set = Query output**

# Core Concept

> **A SQL query uses `SELECT` to specify the fields to retrieve and `FROM` to specify the table containing them. Multiple fields are separated by commas, `*` retrieves all fields, and the query ends with a semicolon.**
