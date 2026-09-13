# Databases

## Course Overview

This course has two main goals:

1. Understand **databases** and how they are structured to store and organize data.
2. Learn how to interact with data in databases using **SQL**.

## Structured Query Language (SQL)

**SQL** stands for **Structured Query Language**.

SQL is the most widely used programming language for communicating with data in databases.

### What SQL Can Do

SQL allows users to:

- Access data quickly.
- Organize data.
- Analyze large amounts of data.
- Retrieve specific information.
- Submit commands to a database through **queries**.

> **SQL query = A command or set of instructions used to access and work with data in a database.**

## What Is a Database?

A **database** is a system used to **store and organize data**.

Compared with spreadsheets, databases can:

- Handle much larger amounts of data.
- Provide stronger security.
- Support multiple users.
- Organize related data across multiple tables.
- Allow users to retrieve information through SQL queries.
- Use security mechanisms such as encryption.

## Library Database Example

Imagine managing data for a library.

The library needs to track:

- Books
- Patrons
- Book checkouts
- Which patron checked out which book

A database could contain:

- `books` table
- `patrons` table
- `checkouts` table

### Example Structure

**Library Database → Books + Patrons + Checkouts**

## Tables

A **table** is a component of a database that organizes related data.

For example, the `patrons` table may contain:

- Library card number
- Name
- Year joined
- Total fines owed

## Rows and Columns

Tables organize data using **rows and columns**.

### Rows

A **row** represents one individual record.

Example:

- One row = One library patron

### Columns

A **column** describes a specific attribute or piece of information about each record.

Example:

- `card_number`
- `name`
- `year_joined`
- `total_fines`

### Simple Concept

**Row = One record**

**Column = One attribute/field**

## Relational Databases

A **relational database** consists of multiple tables that are connected through shared information.

The tables work together through **relationships**.

### Library Example

The database contains:

- `patrons`
- `books`
- `checkouts`

The `checkouts` table can connect to:

- `patrons` through `card_number`
- `books` through `book_id`

### Relationship

**Patrons ← card_number → Checkouts ← book_id → Books**

This allows the database to answer questions involving information from multiple tables.

### Example Question

> How many books did Izzy check out?

The database can connect the relevant patron and checkout records using their shared identifiers.

## Database Relationships

Shared fields allow tables to be related.

| Table | Shared Field | Related Table |
|---|---|---|
| `checkouts` | `card_number` | `patrons` |
| `checkouts` | `book_id` | `books` |

These relationships allow information stored in separate tables to be combined when querying.

## SQL Queries

Users interact with database information by writing **SQL queries**.

A query tells the database:

- What information to retrieve.
- What records to select.
- How to organize or present the results.

### Important Concept

When a database is queried:

> **The stored data does not change simply because it was queried.**

Instead, the database **accesses and presents the data according to the query instructions**.

### Example

A query can request:

- A particular patron.
- All books checked out.
- The number of books checked out.
- Information combining patrons and books.

The result is presented to the user while the underlying stored data remains unchanged.

## Advantages of Databases

### 1. Large-Scale Data Storage

Databases can handle much larger amounts of data than typical spreadsheets.

### 2. Security

Databases can provide stronger security mechanisms, including encryption.

### 3. Structured Organization

Data can be separated into multiple related tables instead of being stored in one large dataset.

### 4. Relationships

Related tables can be connected through shared fields.

### 5. Multiple Users

Many users can query a database simultaneously.

### 6. Data Access Through SQL

SQL provides a standardized way to access and analyze database information.

## Database vs. Spreadsheet

| Feature | Database | Spreadsheet |
|---|---|---|
| **Data volume** | Can handle very large datasets | Better suited to smaller datasets |
| **Structure** | Multiple related tables | Sheets/cells |
| **Relationships** | Designed to connect tables | Possible but less specialized |
| **Security** | Stronger database security capabilities | Generally more limited |
| **Multiple users** | Designed for concurrent access | More limited depending on platform |
| **Querying** | SQL | Spreadsheet formulas/functions |
| **Purpose** | Large-scale organized data management | Data entry, calculations, analysis |

## Exam / Interview Key Points

- **SQL = Structured Query Language**.
- SQL is widely used to communicate with data in databases.
- SQL uses **queries** to access, organize, and analyze data.
- A **database** stores and organizes data.
- A **table** is a component of a database.
- Tables consist of **rows and columns**.
- **Row = individual record**.
- **Column = specific attribute/field**.
- A **relational database** contains multiple tables that are connected through relationships.
- Tables can be related through **shared fields**.
- In the library example:
  - `checkouts.card_number` connects to `patrons.card_number`.
  - `checkouts.book_id` connects to `books.book_id`.
- SQL queries can combine information from multiple related tables.
- Multiple users can query the same database simultaneously.
- Querying a database **does not modify the stored data by itself**; it retrieves and presents information according to the query.
- Databases can handle more data and provide stronger security capabilities than typical spreadsheets.

## Quick Memory Aid

**Database = Stores data**

**Table = Organizes data**

**Row = Record**

**Column = Attribute**

**Relationship = Connects tables**

**SQL = Communicates with the database**

**Query = Requests information**

## Core Concept

> **A database organizes data into tables made up of rows and columns. In a relational database, multiple tables are connected through shared information, and SQL queries are used to retrieve and analyze the data without changing the underlying stored data simply by querying it.**
