# 🔗 Model 1:N Relationships with Foreign Keys

## 1. 🧩 Key Constraints and Relationships

This chapter focuses on using **key constraints** to model relationships between database tables.

The current database contains three entity types with primary keys:

- `professors`
- `organizations`
- `universities`

The `affiliations` table does **not** have a primary key for a specific reason that is addressed in this chapter.

---

# 2. 1:N Relationship

The next relationship to model is between:

`professors` 👨‍🏫  
and  
`universities` 🏫

### 📌 Relationship

Each professor works for **at most one university**.

A university can have **any number of professors**, including zero.

### Cardinality

**Professor → University = N:1**

or equivalently:

**University → Professors = 1:N**

### 💡 Example

One university:

`University A`

can have:

`Professor 1`  
`Professor 2`  
`Professor 3`

But each professor works for **at most one university**.

---

# 3. 🔷 Relationship in an ER Diagram

In an **Entity-Relationship Diagram (ERD)**:

- A **rhombus/diamond** represents a relationship type.
- Small numbers indicate the **cardinality** of the relationship.

### 📌 Cardinality

`Professor → 0..1 University`

`University → 0..N Professors`

A professor can work for **at most one** university.

A university can have **zero or many** professors.

---

# 4. 🔑 Foreign Key

A **foreign key** is a column that points to a **primary key in another table**.

Foreign keys are used to implement relationships between tables.

### Example

`professors.university_shortname`

references:

`universities.id`

So:

`professors.university_shortname → universities.id`

---

# 5. 🛡️ Foreign Key Requirements

A foreign key has important restrictions.

### 1️⃣ Same Domain and Data Type

The foreign key must have the **same domain and data type** as the referenced primary key.

Example:

`professors.university_shortname`

must match the domain/data type of:

`universities.id`

### 2️⃣ Referenced Value Must Exist

A foreign key value must exist as a value in the referenced primary key.

For example, if:

`universities.id = 'EPF'`

exists, then a professor can use:

`university_shortname = 'EPF'`

If the university does not exist, that value cannot be used as a valid foreign key.

This is the **foreign key constraint**, also called:

**Referential Integrity** 🔐

---

# 6. 🔄 Foreign Key vs Primary Key

A foreign key is **not necessarily a key** itself.

Therefore, a foreign key can contain:

- ✅ Duplicate values
- ✅ `NULL` values

### Example

Several professors can work for the same university:

| professor | university_shortname |
|---|---|
| Professor A | EPF |
| Professor B | EPF |
| Professor C | EPF |

`EPF` appears multiple times.

Therefore:

`university_shortname`

is a foreign key but **not a unique key**.

---

# 7. 🏫 Example from the Database

The `professors` table contains:

`university_shortname`

The `universities` table contains:

`id`

These fields have the same domain and data type.

Furthermore, every value in:

`professors.university_shortname`

can be found in:

`universities.id`

Therefore, the requirements for a foreign key are fulfilled.

### 🔁 Example

`professors.university_shortname → universities.id`

Some values may occur multiple times.

For example:

`EPF` → 3 occurrences

`UBE` → 3 occurrences

This confirms that the column is **not itself a key**.

---

# 8. 🏗️ Specifying a Foreign Key

A foreign key can be specified when creating a table.

### Example

First, create a `manufacturers` table with:

`name` as the primary key.

CREATE TABLE manufacturers (
    name VARCHAR(50) PRIMARY KEY
);

Then create a `cars` table.

CREATE TABLE cars (
    model VARCHAR(50) PRIMARY KEY,
    manufacturer VARCHAR(50) REFERENCES manufacturers(name)
);

### 🔗 Relationship

`cars.manufacturer → manufacturers.name`

Only manufacturers that already exist in the `manufacturers` table can be used.

---

# 9. 🛡️ Foreign Key Constraint in Action

Suppose the `manufacturers` table contains:

| name |
|---|
| Toyota |
| Honda |

A valid car:

`Toyota Corolla`

✅ Allowed

A car with:

`Ford`

❌ Not allowed if `Ford` does not exist in `manufacturers`.

### 💡 Key Idea

The foreign key ensures that the referenced value **already exists**.

This protects **referential integrity**.

---

# 10. 🔄 Adding a Foreign Key to an Existing Table

A foreign key can also be added after the table already exists.

The syntax follows the same general pattern used for adding:

- Primary keys
- Unique constraints

### 🧩 Pattern

ALTER TABLE table_name
ADD CONSTRAINT constraint_name
FOREIGN KEY (column_name)
REFERENCES referenced_table (referenced_column);

### Example

ALTER TABLE cars
ADD CONSTRAINT cars_manufacturer_fkey
FOREIGN KEY (manufacturer)
REFERENCES manufacturers(name);

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **1:N Relationship** | One record in one table can relate to many records in another |
| **Professor → University** | Each professor works for at most one university |
| **University → Professors** | A university can have zero or many professors |
| **Foreign Key** | Column that references a primary key in another table |
| `REFERENCES` | Specifies the referenced table and column |
| **Foreign Key Data Type** | Must match the referenced primary key's domain/data type |
| **Referential Integrity** | Only valid referenced primary-key values can be used |
| **Duplicate FK values** | ✅ Allowed |
| **NULL FK values** | ✅ Allowed |
| **Foreign Key ≠ Primary Key** | A foreign key does not have to uniquely identify records |
| `professors.university_shortname` | Foreign key referencing `universities.id` |
| `ADD CONSTRAINT` | Used to add a foreign key to an existing table |

# 💡 Memory Aid

**Primary Key** 🔑  
→ Identifies a record uniquely

**Foreign Key** 🔗  
→ Points to another table's primary key

**`REFERENCES`** 👉  
→ Defines what the foreign key points to

**Referential Integrity** 🛡️  
→ Foreign key values must exist in the referenced primary key

### 1:N Relationship

**One University 🏫 → Many Professors 👨‍🏫**

`universities.id`  
⬇️  
`professors.university_shortname`
