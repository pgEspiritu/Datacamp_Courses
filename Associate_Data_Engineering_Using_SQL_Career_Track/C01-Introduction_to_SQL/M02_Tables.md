# Tables

## Overview

A **table** is the main building block of a database.

Tables organize related data into:

- **Rows**, also called records
- **Columns**, also called fields

Good table design and naming make databases easier to understand, query, and maintain.

## Table Naming

Table names should follow clear and consistent naming conventions.

### Best Practices

- Use a clear name that describes the data stored in the table.
- Use **lowercase**.
- Use **underscores** instead of spaces.
- Choose names that clearly identify the table's contents.

### Examples

Good table names:

- `inventory`
- `products`
- `books`
- `patrons`
- `checkouts`

Avoid names with spaces such as:

- `library books`
- `customer data`

## Records and Fields

In database terminology:

**Row = Record**

**Column = Field**

### Record

A **record** contains the data for **one individual observation/entity**.

Example:

The `patrons` table contains four records if there are four library patrons.

A patron's record might contain:

- Name: Jasmin
- Year joined: 2022
- Fines owed: $2.05

### Field

A **field** contains one specific piece of information for every record in the table.

Example:

The `name` field contains the names of all patrons.

## Record vs. Field

| Database Term | Spreadsheet Equivalent | Meaning |
|---|---|---|
| **Record** | Row | One individual observation/entity |
| **Field** | Column | One type of information about each record |

## Field Naming

Field names are important because they must be referenced when writing SQL queries.

### Best Practices

Field names should:

- Be **lowercase**.
- Use **underscores** instead of spaces.
- Be **singular**.
- Be unique within the table.
- Not have the same name as the table.

### Examples

Good:

- `card_num`
- `name`
- `year_joined`
- `total_fines`

Avoid:

- `card nums`
- `names`
- `patrons` as a field name inside the `patrons` table

### Why Singular?

A field represents the information for **one record**.

Therefore:

**`name`** → Correct

**`names`** → Avoid

**`card_num`** → Correct

**`card_nums`** → Avoid

## Unique Identifiers

A table contains a special field that uniquely identifies each record.

This is often called a **key** or **unique identifier**.

### Requirements

A unique identifier:

- Must identify one specific record.
- Must be **unique for every record**.
- Should not contain duplicate values.

### Example

In the `patrons` table:

**`card_num` = Unique Identifier**

It is better than using `name` as the identifier because two patrons may have the same name.

Example:

| card_num | name |
|---|---|
| 1001 | John Smith |
| 1002 | John Smith |

The names are duplicated, but the `card_num` values are unique.

## Why Names Should Not Be Unique Identifiers

Names are not guaranteed to be unique.

Two or more people can have:

- The same first name.
- The same last name.
- The same first and last name.

A dedicated identifier such as a card number provides a reliable way to distinguish records.

## Multiple Tables

It is often better to store data in **several well-organized, related tables** instead of putting everything into one large table.

### Example

A library database can contain:

- `patrons`
- `checkouts`
- `books`

Instead of combining everything into one large table, each table can contain data relevant to one entity or process.

## Problems with One Large Table

Combining the `patrons` and `checkouts` tables can create:

- Duplicate information.
- Less clear data.
- Repeated values.
- Loss of uniqueness for fields that should identify one record.

### Example

If Izzy checks out two books, Izzy's information may appear twice in a combined table.

The `card_num` value would therefore appear multiple times.

This means:

**`card_num` is no longer unique in the combined checkout data.**

## Why Use Separate Tables?

Separate related tables help:

- Reduce duplicate information.
- Keep data organized.
- Maintain unique identifiers.
- Improve clarity.
- Make relationships easier to manage.
- Make analysis easier.
- Make SQL queries more effective.

### Concept

**Separate Tables + Relationships + SQL = Organized and Flexible Database**

## Database Structure Example

A library database can be organized as:

**`patrons`**

- `card_num`
- `name`
- `year_joined`
- `total_fines`

**`books`**

- `book_id`
- `title`
- Other book information

**`checkouts`**

- `card_num`
- `book_id`
- Other checkout information

The tables can then be connected using shared identifiers.

## Table Design Principles

### Table Names

**Clear + Lowercase + Underscores**

Example:

`library_books`

### Field Names

**Clear + Lowercase + Singular + Underscores**

Example:

`year_joined`

### Records

**One record = One individual observation/entity**

### Fields

**One field = One type of information**

### Unique Identifier

**One key = Uniquely identifies each record**

## Exam / Interview Key Points

- A **table** is a fundamental component of a database.
- Tables are organized into **records and fields**.
- **Rows are records**.
- **Columns are fields**.
- A record contains data about one individual observation/entity.
- A field contains one piece of information for every record.
- Table names should be:
  - Clear
  - Lowercase
  - Written with underscores instead of spaces
- Field names should be:
  - Clear
  - Lowercase
  - Singular
  - Written with underscores instead of spaces
  - Unique within the table
  - Different from the table name
- Tables contain a **unique identifier/key** for each record.
- A unique identifier must be **unique for every record**.
- Names are generally poor unique identifiers because different people can have the same name.
- Using several related tables is often better than putting everything into one large table.
- Separate tables reduce duplicate information and improve organization.
- SQL can be used to connect and analyze related tables.

## Quick Memory Aid

**Table = Collection of records**

**Record = One row**

**Field = One column**

**Key = Unique identifier**

**Good table name = lowercase + descriptive + underscores**

**Good field name = lowercase + singular + underscores**

**Better database design = Multiple related tables instead of one giant table**

## Most Important Concept

> **Well-designed database tables use clear naming conventions, organize data into records and fields, and include unique identifiers for each record. Using multiple related tables instead of one large table reduces duplication, preserves organization, and makes SQL-based analysis easier.**
