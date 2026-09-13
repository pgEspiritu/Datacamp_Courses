# 🛠️ Update Your Database as the Structure Changes

## 1. 🗄️ Current Database Structure

The database now consists of **five different tables**.

The next step is to **migrate the data** from the original table into the new tables.

---

# 2. 📊 Current Database Model

The current **entity-relationship diagram (ERD)** shows five tables.

At this point:

✅ `university_professors` contains the data  
❌ The other four tables are still empty

The goal is to migrate the different **entity types** from:

`university_professors`

into their appropriate new tables.

Eventually, the original `university_professors` table can be **deleted**.

---

# 3. 🔁 Store Only DISTINCT Data

One major advantage of splitting the original table into multiple tables is **reducing redundancy**.

The original `university_professors` table contains:

`1377` entries

But there are only:

`1287` distinct organizations

Therefore, the new `organizations` table only needs to store:

`1287` distinct organizations

### 💡 Key Idea

**Do not migrate duplicate records when the new table should contain unique entities.**

---

# 4. 📥 `INSERT INTO SELECT DISTINCT`

To copy distinct data from an existing table into a new table, use:

`INSERT INTO ... SELECT DISTINCT`

### 🧩 Pattern

INSERT INTO target_table
SELECT DISTINCT column
FROM source_table;

### Example

INSERT INTO organizations
SELECT DISTINCT organization
FROM university_professors;

This copies only the **unique organizations** into `organizations`.

### ⚠️ Without `DISTINCT`

Using:

`INSERT INTO ... SELECT`

without `DISTINCT` would copy duplicate records as well.

---

# 5. 📝 Normal `INSERT INTO`

The normal use of `INSERT INTO` is to manually insert values into a table.

### 🧩 Pattern

INSERT INTO table_name (column1, column2)
VALUES (value1, value2);

### 📌 Structure

`INSERT INTO` → target table

`(column1, column2)` → optional columns to fill

`VALUES` → actual values to insert

---

# 6. ✏️ Rename a Column

Before migrating data, the `affiliations` table needs to be corrected.

The column:

`organisation`

uses a spelling inconsistent with the American-style spelling used by the table:

`organizations`

It should be renamed using:

`ALTER TABLE`

and:

`RENAME COLUMN`

### 🧩 Syntax

ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;

### Example

ALTER TABLE affiliations
RENAME COLUMN organisation TO organization;

### 💡 Memory Aid

**RENAME COLUMN = old name → new name** 🔄

---

# 7. 🗑️ Drop a Column

The `affiliations` table also contains:

`university_shortname`

This column is not needed and should be removed.

Use:

`DROP COLUMN`

### 🧩 Syntax

ALTER TABLE table_name
DROP COLUMN column_name;

### Example

ALTER TABLE affiliations
DROP COLUMN university_shortname;

### ⚠️ Important

Dropping the column is straightforward while the table is still **empty**.

---

# 8. 🔑 Identifying a Professor

A query showed:

`551` unique combinations of:

- `firstname`
- `lastname`
- `university_shortname`

A second query showed:

`551` unique combinations of:

- `firstname`
- `lastname`

### ✅ Conclusion

`firstname + lastname`

are sufficient to **uniquely identify a professor** in this database.

Therefore:

`university_shortname`

is not needed to identify a professor in the `affiliations` table.

---

# 9. 🔗 Affiliations Table

The affiliation of a professor with an organization only needs:

- `firstname`
- `lastname`
- `function`
- `organization`

### 📌 Structure

`professor → organization`

with:

`function` = the role of the professor at that organization

### ✅ Example

A professor may have:

`firstname + lastname + function + organization`

This is enough to represent the affiliation.

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Data migration** | Moving data from the original table into the new tables |
| **Redundancy** | Reduced by separating entity types into different tables |
| `DISTINCT` | Prevents duplicate records from being copied |
| `INSERT INTO SELECT DISTINCT` | Copies unique data from an existing table |
| `INSERT INTO` | Manually inserts values into a table |
| `VALUES` | Specifies the values to insert |
| `ALTER TABLE` | Changes the structure of an existing table |
| `RENAME COLUMN` | Renames an existing column |
| `DROP COLUMN` | Deletes a column |
| `firstname + lastname` | Uniquely identifies a professor in this database |
| `university_shortname` in `affiliations` | Not needed to identify the professor |
| `affiliations` | Stores the relationship between professors and organizations |
| `function` | Describes the professor's role at the organization |

# 💡 Memory Aid

**Migrate Unique Data** → `INSERT INTO ... SELECT DISTINCT` 📥

**Rename a Column** → `ALTER TABLE ... RENAME COLUMN ... TO ...` ✏️

**Remove a Column** → `ALTER TABLE ... DROP COLUMN ...` 🗑️

**Professor Identifier** → `firstname + lastname` 🔑

**Affiliation** → `firstname + lastname + function + organization` 🔗
