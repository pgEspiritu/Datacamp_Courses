# SQL Databases

## SQL Overview

**SQL** stands for **Structured Query Language**.

SQL is the primary language used to interact with **RDBMS (Relational Database Management Systems)**.

An RDBMS is a database system that contains multiple related tables.

### Why SQL Is Important

SQL allows users to:

- Access many records at once.
- Filter records.
- Group records.
- Aggregate records.
- Create databases and tables.
- Update and maintain databases.
- Query and retrieve data.

SQL is widely used because it is:

- Powerful for handling large sets of records.
- Relatively easy to read and write.
- Similar to natural English in its syntax.

## SQL and Data Roles

### Data Engineers

Data engineers use SQL to:

- Create tables.
- Create and maintain databases.
- Define columns and data types.
- Update tables.
- Insert records.
- Transform data.

### Data Scientists

Data scientists use SQL primarily to:

- Query databases.
- Retrieve information.
- Filter records.
- Select specific columns.

### Key Difference

**Data Engineer → Creates and maintains the database**

**Data Scientist → Queries and analyzes the database**

## SQL Data Types

When creating a table, each column is assigned a data type.

Common examples from the Spotflix employee table:

| Data Type | Purpose | Example |
|---|---|---|
| **INTEGER** | Whole numbers without decimals | `1001` |
| **VARCHAR** | Variable-length text | `Engineering` |
| **BOOLEAN** | Logical value | `TRUE` / `FALSE` |

### VARCHAR

`VARCHAR` stands for **Variable Characters**.

For example, `VARCHAR(255)` means the text value can contain a maximum of **255 characters**.

### BOOLEAN

A Boolean represents a logical value:

- `TRUE`
- `FALSE`

In the example presented in the course, Boolean values can be represented as:

- `0` = False
- `1` = True

## SQL for Data Engineers

A data engineer can use SQL to create a table.

Conceptually:

`CREATE TABLE employees`

The table can contain columns such as:

- `employee_id`
- `first_name`
- `last_name`
- `role`
- `team`
- `full_time`
- `office`

Each column has an appropriate data type.

Example structure:

| Column | Data Type |
|---|---|
| `employee_id` | INTEGER |
| `first_name` | VARCHAR |
| `last_name` | VARCHAR |
| `role` | VARCHAR |
| `team` | VARCHAR |
| `full_time` | BOOLEAN |
| `office` | VARCHAR |

After creating the table, data engineers can use SQL statements to:

- Update the table.
- Insert records.
- Maintain the data.

## SQL for Data Scientists

Data scientists use SQL to query tables.

For example, Julian wants the **first and last names of employees whose role contains the word "data"**.

The query conceptually uses:

- `SELECT` → Choose the columns.
- `FROM` → Specify the table.
- `WHERE` → Filter the records.

Conceptually:

`SELECT first_name, last_name FROM employees WHERE role LIKE '%Data%'`

### Important SQL Concepts

**SELECT** = choose columns/data to retrieve

**FROM** = specify the source table

**WHERE** = filter records

**LIKE** = search for a matching text pattern

`%` = wildcard that allows text to appear before or after the specified value

Therefore:

`'%Data%'`

means **"Data" can appear anywhere in the role title**.

## Database Schema

A database contains multiple tables.

A **database schema** defines how these tables are structured and **how they are related to each other**.

### Example: Spotflix Database

Spotflix can have tables for:

- Albums
- Artists
- Songs
- Playlists
- Users
- Genres
- Labels

## Table Relationships

### Artists and Albums

The **Artists** table contains:

- Artist ID
- Artist name
- Biography

The **Albums** table contains:

- Album ID
- Artist ID
- Album title
- Other album information

The tables are related through:

**Artist ID**

### Albums and Songs

The **Songs** table contains:

- Song ID
- Album ID
- Song title
- Other song information

The Songs table is related to Albums through:

**Album ID**

### Songs and Playlists

The **Playlists** table contains:

- Playlist ID
- User ID
- Song ID
- Other playlist information

The Playlists table can be related to Songs through:

**Song ID**

### Simplified Relationship

**Artists → Albums → Songs → Playlists**

Relationships:

- Artists ↔ Albums = `artist_id`
- Albums ↔ Songs = `album_id`
- Songs ↔ Playlists = `song_id`

This interconnected structure is why they are called **relational databases**.

## Relational Database Management System (RDBMS)

An **RDBMS** is a database management system that organizes data into related tables.

Key characteristics:

- Data is organized into tables.
- Tables contain rows and columns.
- Tables can be related using common identifiers.
- SQL is used to interact with the database.

## SQL Implementations

There are multiple implementations of SQL.

They are generally very similar, although some syntax and features differ.

Examples include:

- PostgreSQL
- MySQL
- Microsoft SQL Server
- Oracle Database
- SQLite

> Switching between SQL implementations is similar to switching between QWERTY and AZERTY keyboards or British and American English: some things change, but the fundamentals remain similar.

## Exam / Interview Key Points

- **SQL = Structured Query Language**.
- SQL is the reference language for **RDBMS**.
- **RDBMS = Relational Database Management System**.
- RDBMS organizes data into **related tables**.
- SQL can retrieve, filter, group, aggregate, create, and maintain data.
- **Data engineers** use SQL to create and maintain databases.
- **Data scientists** use SQL primarily to query databases.
- `CREATE TABLE` is used to create a table.
- `SELECT` chooses the data/columns to retrieve.
- `FROM` identifies the table being queried.
- `WHERE` filters records.
- `LIKE` can be used for pattern matching.
- `%` is a wildcard used with `LIKE`.
- `INTEGER` stores whole numbers.
- `VARCHAR` stores variable-length text.
- `BOOLEAN` stores logical values such as true/false.
- `VARCHAR(255)` allows up to 255 characters.
- A **database schema** defines the structure and relationships between tables.
- Tables can be related using identifiers such as:
  - `artist_id`
  - `album_id`
  - `song_id`

## Quick Memory Aid

**SQL = Talk to the database**

**RDBMS = Related tables**

**Data Engineer = Build / Maintain**

**Data Scientist = Query / Analyze**

**SQL Basics:**

- `SELECT` → What do I want?
- `FROM` → Where is it?
- `WHERE` → Which records?
- `LIKE` → Does it match this pattern?

## Core Concept

> **SQL is the primary language used to interact with relational databases, allowing data engineers to create and maintain databases and data scientists to query and analyze the data stored in them.**
