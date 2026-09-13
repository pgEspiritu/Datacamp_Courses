# 🔑 Primary Keys

## 1. 🎯 What Is a Primary Key?

A **primary key** is one of the most important concepts in database design.

Almost every database table should have a **primary key**.

A primary key is chosen from the table's **candidate keys**.

### Main Purpose

The primary key's main purpose is to:

**Uniquely identify each record in a table.** 🔑

This also makes it easier to **reference records from other tables**.

---

# 2. ✅ Requirements of a Primary Key

A primary key must be defined on columns that:

- ❌ Do not allow duplicate values
- ❌ Do not allow `NULL` values

Therefore:

**Primary Key = UNIQUE + NOT NULL** ✅

### 📌 Time-Invariant Constraint

Primary key constraints must hold:

- For the **current data**
- For **all future data**

This is called **time-invariant**.

Therefore, choose columns whose values are expected to **always remain unique and non-NULL**.

---

# 3. 🏗️ Defining a Primary Key During Table Creation

A primary key can be defined directly in the column definition.

### Example

CREATE TABLE universities (
    university_id INTEGER PRIMARY KEY,
    university_name VARCHAR(100)
);

Here:

`university_id`

is the primary key.

---

# 4. 🔗 Composite Primary Key

A primary key can also consist of **more than one column**.

This is called a **composite primary key**.

### Example

CREATE TABLE example (
    column1 INTEGER,
    column2 INTEGER,
    PRIMARY KEY (column1, column2)
);

The combination:

`column1 + column2`

forms **one primary key**.

### ⚠️ Important

Even when multiple columns are used:

**There is still only ONE primary key.**

The key is formed by the **combination of the columns**.

---

# 5. 🎯 Keep Primary Keys Small

Ideally, a primary key should consist of **as few columns as possible**.

### 💡 Memory Aid

**Fewer columns → Simpler primary key** ✅

---

# 6. ➕ Adding a Primary Key to an Existing Table

A primary key can also be added after a table has already been created.

The procedure is similar to adding a `UNIQUE` constraint.

Use:

`ADD CONSTRAINT`

### 🧩 Syntax

ALTER TABLE table_name
ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);

### Example

ALTER TABLE universities
ADD CONSTRAINT universities_pkey
PRIMARY KEY (university_id);

### 📌 Important

When adding a primary key to an existing table:

- The constraint needs a **name**.
- The selected column(s) must satisfy the primary key requirements.

---

# 7. 🗄️ Primary Keys in the Current Database

In the database used in the course, primary keys will be added to:

- `universities`
- `organizations`
- `professors`

### 🔑 Key Types

`universities` → Primary key

`organizations` → Primary key

`professors` → **Surrogate key**

---

# 8. 🆔 Surrogate Key

A **surrogate key** is a special type of primary key.

The `professors` table will receive a surrogate key in the final part of this chapter.

The primary key will be added as a new attribute:

`id`

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Primary Key** | Uniquely identifies records in a table |
| **Candidate Key** | A possible key from which a primary key can be chosen |
| **Primary Key Purpose** | Unique record identification and easier referencing from other tables |
| **Primary Key Values** | Must not be duplicate |
| **Primary Key NULLs** | Not allowed |
| **Time-invariant** | Constraint must hold for current and future data |
| **Composite Primary Key** | One primary key formed from multiple columns |
| **Primary Key Size** | Ideally uses as few columns as possible |
| `PRIMARY KEY` | Defines a primary key |
| `ADD CONSTRAINT` | Used to add a primary key to an existing table |
| **Surrogate Key** | A special type of primary key |
| `id` | Surrogate key to be added to `professors` |

# 💡 Memory Aid

**Primary Key = Unique + Not NULL + Stable** 🔑

**One column:**  
`column PRIMARY KEY`

**Multiple columns:**  
`PRIMARY KEY (column1, column2)`

**Existing table:**  
`ALTER TABLE → ADD CONSTRAINT → PRIMARY KEY`

**Professor table:**  
`id` → Surrogate Key 🆔
