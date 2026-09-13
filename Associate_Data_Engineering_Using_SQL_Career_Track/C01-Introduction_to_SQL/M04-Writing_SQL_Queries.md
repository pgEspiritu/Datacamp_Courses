# Writing SQL Queries

## Overview

This lesson introduces additional SQL keywords and concepts that make queries more useful and reusable:

- **Aliasing**
- **DISTINCT**
- **Views**

# 1. Aliasing

**Aliasing** allows you to temporarily rename a column in the **result set**.

The original column name in the database table is **not changed**.

### AS Keyword

Use the `AS` keyword to assign an alias.

Example:

`SELECT name AS first_name FROM employees;`

This changes the column name shown in the result set from:

`name`

to:

`first_name`

### Important

**Alias = New name only in the query result**

The actual database field remains:

`name`

### Why Use Aliasing?

Aliasing can make result sets:

- Clearer
- Easier to understand
- More concise
- More suitable for reporting

# 2. DISTINCT

The **DISTINCT** keyword is used to return **unique values** and remove duplicate records from the result set.

### Example

Suppose the `employees` table contains:

`year_hired`

with values:

`2020, 2021, 2021, 2022, 2022, 2023`

Using:

`SELECT year_hired FROM employees;`

returns duplicate years.

Using:

`SELECT DISTINCT year_hired FROM employees;`

returns each year only once.

Result:

`2020, 2021, 2022, 2023`

### Key Concept

**DISTINCT = Remove duplicate result values**

It does not delete or modify the original data in the table.

# 3. DISTINCT with Multiple Fields

`DISTINCT` can be applied to multiple fields.

In this case, SQL returns **unique combinations of the selected fields**.

Example:

`SELECT DISTINCT dept_id, year_hired FROM employees;`

SQL considers the combination of:

`dept_id + year_hired`

when determining whether a row is duplicated.

### Important Concept

`DISTINCT` does **not** necessarily make each individual column unique.

Instead:

> It removes duplicate **combinations of all selected fields**.

### Example

Suppose the data is:

| dept_id | year_hired |
|---:|---:|
| 3 | 2021 |
| 3 | 2021 |
| 3 | 2022 |
| 4 | 2021 |
| 4 | 2022 |

Using:

`SELECT DISTINCT dept_id, year_hired FROM employees;`

returns:

| dept_id | year_hired |
|---:|---:|
| 3 | 2021 |
| 3 | 2022 |
| 4 | 2021 |
| 4 | 2022 |

Notice that:

- `dept_id = 3` appears multiple times.
- `year_hired = 2021` appears multiple times.

But every **combination of `dept_id` and `year_hired` is unique**.

# 4. Views

A **view** is a **saved SQL query that behaves like a virtual table**.

A view does not store the query results as separate data.

Instead, it stores the **SQL query itself**.

### Key Characteristics

- Acts like a virtual table.
- Stores the query rather than a separate copy of the data.
- Can be queried like a regular table.
- Results reflect the latest changes in the underlying database.
- Useful for saving and reusing commonly used queries.

> **View = Saved SQL query + Virtual table**

# 5. Creating a View

The basic syntax uses:

- `CREATE VIEW`
- View name
- `AS`
- SQL query

General pattern:

`CREATE VIEW view_name AS SELECT ... FROM ...;`

Example:

`CREATE VIEW employee_hire_years AS SELECT DISTINCT year_hired FROM employees;`

This creates a view called:

`employee_hire_years`

The view contains the saved query rather than a separate stored copy of the results.

### Important

Creating a view **does not produce a result set**.

It only saves the query for later use.

# 6. Querying a View

Once a view has been created, it can be queried like a normal table.

Example:

`SELECT * FROM employee_hire_years;`

You can therefore think of a view as a **virtual table generated from a saved query**.

# 7. View Example

Suppose we frequently need the unique years in which employees were hired.

Instead of repeatedly writing:

`SELECT DISTINCT year_hired FROM employees;`

we can create:

`CREATE VIEW employee_hire_years AS SELECT DISTINCT year_hired FROM employees;`

Then later use:

`SELECT * FROM employee_hire_years;`

### Benefit

The query is saved and can be reused without rewriting it every time.

Because the view is based on the underlying table, its results can reflect **new database changes**.

# SQL Concepts Summary

| Concept | Purpose | Example |
|---|---|---|
| **AS** | Assigns an alias to a column | `name AS first_name` |
| **DISTINCT** | Removes duplicate result values/combinations | `DISTINCT year_hired` |
| **CREATE VIEW** | Saves a SQL query as a virtual table | `CREATE VIEW employee_hire_years AS ...` |
| **VIEW** | Saved query that can be queried like a table | `SELECT * FROM employee_hire_years;` |

# Aliasing vs. Changing a Column Name

Aliasing:

`SELECT name AS first_name FROM employees;`

Changes the name **only in the result set**.

It does **not** rename the actual database column.

### Remember

**Alias = Temporary/result-set name**

**Actual field name = Unchanged**

# DISTINCT vs. DELETE

`DISTINCT`:

- Removes duplicate values **from the query result**.
- Does not modify the underlying table.
- Does not delete records.

`DELETE`:

- Removes records from a table.
- Modifies stored data.

> `DISTINCT` is for controlling query output, not for deleting duplicate data from the database.

# View vs. Table

| Feature | Table | View |
|---|---|---|
| **Stores data** | Yes | No separate copy of data |
| **Stores query** | No | Yes |
| **Virtual** | No | Yes |
| **Can be queried with SELECT** | Yes | Yes |
| **Reflects underlying database changes** | Contains stored data | Query results reflect underlying changes |

# Exam / Interview Key Points

- **Aliasing** renames a column in the query result.
- `AS` is used to create an alias.
- Aliasing does **not** change the original column name.
- **DISTINCT** returns unique values.
- `DISTINCT` removes duplicates from the **result set**, not the underlying table.
- `DISTINCT` can be applied to multiple fields.
- With multiple fields, `DISTINCT` returns unique **combinations** of those fields.
- Individual columns can still contain repeated values when using multiple fields with `DISTINCT`.
- A **view** is a saved SQL query.
- A view acts like a **virtual table**.
- A view stores the **query**, not a separate copy of the result data.
- Views can provide results based on the latest changes to the underlying database.
- `CREATE VIEW` is used to create a view.
- `AS` defines the query that the view stores.
- Creating a view **does not produce a result set**.
- A view can be queried using `SELECT` just like a table.

# Quick Memory Aid

**AS = Rename in the result**

**DISTINCT = Unique results**

**Multiple DISTINCT fields = Unique combinations**

**VIEW = Saved query**

**CREATE VIEW = Save the query**

**SELECT FROM view = Use the saved query**

# Core Concept

> **Aliasing changes how a column is displayed in the result set, `DISTINCT` removes duplicate values or combinations from query results, and a view saves a SQL query as a virtual table that can be reused and queried like a regular table.**
