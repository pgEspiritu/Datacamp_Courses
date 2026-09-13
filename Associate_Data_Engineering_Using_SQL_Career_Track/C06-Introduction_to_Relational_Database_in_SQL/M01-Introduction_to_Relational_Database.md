# 📚 Introduction to Relational Databases

## 1. 🗄️ Your First Database

Welcome to the course **Introduction to Relational Databases**.

The course explains why **relational databases** have advantages over **flat files** such as:

- CSV files
- Excel sheets

### 🎯 Course Goals

You will learn how to:

- Create relational databases
- Use the main features of relational databases
- Maintain data quality using database concepts

---

## 2. 🏫 Investigating Universities in Switzerland

A data journalism investigation focused on the **secondary employment of Swiss university professors**.

### 🔎 Investigation

The investigation found:

- Many university professors had additional jobs outside their university duties.
- Some were paid by large companies such as **banks and insurance companies**.
- More than **1,500 external employments** were discovered.
- The information was visualized in an interactive graphic.

### ⚠️ Data Challenges

The data came from **various sources with varying quality**.

The database needed to account for relationships such as:

- A professor can work for **different universities**.
- A professor can work for **different companies**.
- A company can employ **multiple professors**.

### 🗃️ Why Use a Database?

A database was used to ensure that:

- Data quality was good.
- Data quality stayed good throughout the process.
- Complex relationships between entities could be represented.

The complex database design was divided into multiple **tables**.

---

## 3. 🔗 What is a Relational Database?

A relational database models **real-life entities** by storing them in tables.

### 📌 Entity

Examples of entities include:

- Professors 👨‍🏫
- Universities 🏫
- Companies 🏢

### 📊 Table Design

Each table contains data from **one entity type**.

For example:

`professors` → professor information

`universities` → university information

`companies` → company information

### ✅ Advantages

#### 1. Reduces Redundancy

Entities are stored **only once**.

For example, a company's details only need to be stored in one row rather than repeatedly for every professor working there.

#### 2. Models Relationships

A relational database can define **how entities relate to one another**.

Example:

`Professor → Multiple Universities`

`Professor → Multiple Companies`

`Company → Multiple Professors`

---

## 4. 🎯 Throughout the Course

The course uses the **same real-life data** from the investigation.

You start with a **single table containing the data** and progressively build a complete relational database.

### 🧱 Database Development

You will build the database:

`Single Table → Columns → Tables → Relational Database`

### 🔑 Important Concepts

You will learn about:

- **Constraints**
- **Keys**
- **Referential Integrity**

These concepts help **preserve data quality** in databases.

### 💡 SQL

A basic understanding of **SQL** is required.

SQL can be used not only to:

- Query data 🔎

but also to:

- Build databases 🏗️
- Maintain databases 🔧

---

## 5. 🐘 Your First PostgreSQL Database

A **PostgreSQL database** has already been created for the course.

It contains a **single table with all the raw data**.

The first exercises involve inspecting this database.

---

## 🔍 `information_schema`

PostgreSQL provides a special database structure called:

`information_schema`

It is a type of **meta-database** that contains information about the current database.

### 📌 What is a Meta-Database?

It stores information **about the database itself**.

For example, it contains information about:

- Tables
- Columns
- Other database metadata

### 🌐 Not PostgreSQL-Specific

`information_schema` is **not specific to PostgreSQL**.

It is also available in other database management systems such as:

- MySQL
- SQL Server

---

## 📋 `information_schema.tables`

The `information_schema` contains different tables of metadata.

One of them is:

`information_schema.tables`

This table contains information about the **tables in the database**.

### Example

`SELECT * FROM information_schema.tables;`

This can be used to inspect the tables available in the database.

---

## 🧩 `information_schema.columns`

The `information_schema` also contains:

`information_schema.columns`

This table contains information about **columns** in database tables.

Once you know the name of a table, you can query `information_schema.columns` to inspect its columns.

### Example

`SELECT * FROM information_schema.columns;`

---

## 📌 Example: Inspecting `pg_config`

The system table:

`pg_config`

has only **two columns**.

These columns are used for storing **name-value pairs**.

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Relational Database** | Stores real-life entities in related tables |
| **Entity** | A real-life object represented in a database |
| **Table** | Contains data for an entity type |
| **Redundancy** | Reduced by storing entities only once |
| **Relationships** | Define how entities relate to each other |
| **Constraints** | Help preserve data quality |
| **Keys** | Help identify and relate records |
| **Referential Integrity** | Helps maintain valid relationships |
| **PostgreSQL** | Database management system used in the course |
| `information_schema` | Meta-database containing information about the current database |
| `information_schema.tables` | Contains information about database tables |
| `information_schema.columns` | Contains information about table columns |
| `pg_config` | Example system table with two columns |

## 💡 Memory Aid

**Relational Database = Entities + Tables + Relationships** 🔗

**`information_schema` = Information about the Database** 🔍

**`tables` → Tables** 📋  
**`columns` → Columns** 🧩
