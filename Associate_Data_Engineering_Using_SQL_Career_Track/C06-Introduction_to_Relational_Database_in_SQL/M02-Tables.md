# 📊 Tables: At the Core of Every Database

## 1. 🧱 Tables

Tables are one of the **most important concepts** behind databases.

A database can be designed using multiple tables to represent different **entity types** and their relationships.

---

# 2. ⚠️ Redundancy in `university_professors`

The original `university_professors` table contains **redundant data**.

For example:

- The same professor can appear in multiple records.
- The professor's university can also be repeated.
- The professor may have affiliations with multiple organizations.

### 🔁 Why Does Redundancy Occur?

The table contains data belonging to **multiple entity types**.

---

# 3. 🧩 Entity Types in `university_professors`

The original table contains at least three entity types:

| Entity Type | Example |
|---|---|
| 👨‍🏫 Professors | Professor information |
| 🏫 Universities | University information |
| 🏢 Organizations | Third-party organizations |

There is also an attribute:

`function`

This describes the **role a professor has at a particular organization**.

---

# 4. 🔗 Entity-Relationship Diagram (ERD)

The database model can be represented using an:

**Entity-Relationship Diagram (ERD)**

### ERD Symbols

| Symbol | Meaning |
|---|---|
| ⬜ Square | Entity type |
| ⭕ Circle | Attribute / column |

The original database modeled everything as one entity type:

`university_professors`

However, the table actually contains multiple entity types.

---

# 5. ✅ Better Database Model: Three Entity Types

A better design separates the entity types into their own tables:

### `professors`

Stores information about professors.

### `universities`

Stores information about universities.

### `organizations`

Stores information about organizations.

### 🎯 Benefit

This reduces **redundancy** because each professor only needs to be stored **once**.

The professor's university can be represented through:

`university_shortname`

---

# 6. 🔗 Adding Affiliations

The database also stores **professor affiliations with third-party organizations**.

The `function` attribute describes the professor's role in that organization.

### Example

A professor may act as:

`Chairman`

for a third-party organization.

Instead of storing this repeatedly in the original table, affiliations can have their own table.

---

# 7. 🗂️ Four Entity Types

The improved database model contains four tables:

| Table | Purpose |
|---|---|
| `professors` | Stores professor information |
| `universities` | Stores university information |
| `organizations` | Stores organization information |
| `affiliations` | Connects professors with organizations and stores their function |

### 🔗 Relationship

`professors → affiliations ← organizations`

The `affiliations` table connects professors with organizations and describes their role through `function`.

---

# 8. 🏗️ Creating Tables with `CREATE TABLE`

SQL uses:

`CREATE TABLE`

to create a new table.

### Basic Structure

CREATE TABLE table_name (
    column_name data_type
);

At minimum, `CREATE TABLE` requires:

- A **table name**
- One or more **columns**
- A **data type** for each column

---

# 9. 🧪 Example: Creating a Table

A `weather` table could contain three columns with different data types.

CREATE TABLE weather (
    location TEXT,
    temperature NUMERIC,
    country_code CHAR(5)
);

### 📌 Column Definition

Each column requires:

`column_name + data_type`

Example:

`temperature NUMERIC`

---

# 10. 📚 Data Types

SQL supports many different data types.

The lesson introduces examples such as:

| Data Type | Purpose |
|---|---|
| `TEXT` | Stores text |
| `NUMERIC` | Stores numeric values |
| `CHAR(5)` | Stores fixed-length character strings of 5 characters |

More data types will be discussed later in the course.

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Table** | Stores data about an entity type |
| **Entity Type** | A type of real-world entity represented in the database |
| **Redundancy** | Repeated data that can be reduced through better database design |
| `university_professors` | Original table containing multiple entity types |
| `professors` | Separate table for professor entities |
| `universities` | Separate table for university entities |
| `organizations` | Separate table for organization entities |
| `affiliations` | Connects professors with organizations and stores their function |
| **ERD** | Entity-Relationship Diagram |
| ⬜ Square | Entity type in an ERD |
| ⭕ Circle | Attribute / column in an ERD |
| `CREATE TABLE` | Creates a new table |
| **Column** | Requires a name and data type |
| `TEXT` | Text data type |
| `NUMERIC` | Numeric data type |
| `CHAR(5)` | Fixed-length 5-character string |

## 💡 Memory Aid

**One Table with Many Entities → Redundancy 🔁**

**Separate Entity Types → Better Database Design ✅**

`professors` 👨‍🏫  
`universities` 🏫  
`organizations` 🏢  
`affiliations` 🔗

**CREATE TABLE = Table Name + Columns + Data Types** 🏗️
