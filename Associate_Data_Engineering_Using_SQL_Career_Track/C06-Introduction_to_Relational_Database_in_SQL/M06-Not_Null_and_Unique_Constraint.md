# 🛡️ NOT NULL and UNIQUE Constraints

## 1. 🔐 Special Attribute Constraints

Two important **attribute constraints** are:

- `NOT NULL`
- `UNIQUE`

These constraints help improve **data quality** by controlling which values can be stored in columns.

---

# 2. 🚫 NOT NULL Constraint

The `NOT NULL` constraint **disallows `NULL` values** in a column.

### 📌 Important

The constraint applies to:

- The **current state** of the database
- Any **future data** inserted into the database

Therefore, a column can only be given a `NOT NULL` constraint if it **currently contains no `NULL` values**.

### Example

CREATE TABLE students (
    ssn INTEGER NOT NULL,
    lastname VARCHAR(64) NOT NULL
);

This means:

`ssn` → cannot be `NULL` ❌

`lastname` → cannot be `NULL` ❌

---

# 3. ❓ What Does `NULL` Mean?

`NULL` does not have one single meaning.

Depending on the situation, `NULL` can mean:

- The value is **unknown** ❓
- The value **does not exist** 🚫
- The value **does not apply** to the column ➖

### ⚠️ Important

Two `NULL` values do **not necessarily mean the same thing**.

For example:

- A phone number may be unknown.
- A student may not have a phone.
- An office phone may not apply because the student has no office.

All of these can be represented by `NULL`, even though their underlying meanings differ.

---

# 4. 📱 Example: `NULL` Values

Suppose we have a `students` table:

| Column | Can be `NULL`? | Reason |
|---|---|---|
| `ssn` | ❌ No | Should be known for every student |
| `lastname` | ❌ No | Should apply to every student |
| `home_phone` | ✅ Yes | May be unknown or may not exist |
| `office_phone` | ✅ Yes | May not apply to a student |

By default, columns allow `NULL` values unless a constraint prevents them.

---

# 5. ⚠️ Comparing `NULL`

`NULL` represents an unknown or unavailable value.

Therefore, comparing:

`NULL = NULL`

does **not** produce `TRUE`.

In the lesson:

**Comparing `NULL` with `NULL` results in `FALSE`.**

### 💡 Key Idea

Do not assume:

`NULL = NULL`

means the two missing values have the same meaning.

---

# 6. ➕ Add a NOT NULL Constraint

When creating a table, place:

`NOT NULL`

after the column definition.

### 🧩 Syntax

CREATE TABLE table_name (
    column_name data_type NOT NULL
);

### Example

CREATE TABLE students (
    ssn INTEGER NOT NULL,
    lastname VARCHAR(64) NOT NULL
);

---

# 7. 🔄 Add NOT NULL to an Existing Column

Use:

`ALTER COLUMN SET NOT NULL`

### 🧩 Syntax

ALTER TABLE table_name
ALTER COLUMN column_name SET NOT NULL;

### Example

ALTER TABLE students
ALTER COLUMN lastname SET NOT NULL;

### ⚠️ Requirement

The column must contain **no `NULL` values** before the constraint can be added.

---

# 8. 🗑️ Remove a NOT NULL Constraint

Use:

`ALTER COLUMN DROP NOT NULL`

### 🧩 Syntax

ALTER TABLE table_name
ALTER COLUMN column_name DROP NOT NULL;

### Example

ALTER TABLE students
ALTER COLUMN lastname DROP NOT NULL;

---

# 9. 🔢 UNIQUE Constraint

The `UNIQUE` constraint prevents **duplicate values** in a column.

Each value in that column can occur only once.

### Example

A university's short name should be unique:

`university_shortname`

because storing the same university more than once would create unnecessary redundancy.

---

# 10. ⚠️ When UNIQUE Makes Sense

### ✅ Good Candidate

`university_shortname`

Each university should have a unique short name.

### ❌ Not a Good Candidate

`university_city`

Multiple universities can exist in the **same city**.

Therefore:

`university_city` → does not need to be unique.

---

# 11. 🏗️ Create a UNIQUE Constraint

When creating a table, add:

`UNIQUE`

after the column definition.

### 🧩 Syntax

CREATE TABLE universities (
    university_shortname VARCHAR(20) UNIQUE
);

### 📌 Important

A `UNIQUE` constraint can only be added if the column **does not already contain duplicates**.

---

# 12. ➕ Add UNIQUE to an Existing Table

For an existing table, use:

`ADD CONSTRAINT`

### 🧩 Syntax

ALTER TABLE table_name
ADD CONSTRAINT constraint_name UNIQUE (column_name);

### Example

ALTER TABLE universities
ADD CONSTRAINT unique_university_shortname
UNIQUE (university_shortname);

### 💡 Important

Adding a constraint to an existing table uses a different pattern:

`ADD CONSTRAINT`

This pattern will also be used for other constraints later in the course.

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| `NOT NULL` | Prevents `NULL` values |
| `UNIQUE` | Prevents duplicate values |
| `NULL` | Can represent unknown, nonexistent, or inapplicable values |
| NOT NULL before adding | Existing column must have no `NULL` values |
| UNIQUE before adding | Existing column must have no duplicates |
| Create NOT NULL | Add `NOT NULL` after the column definition |
| Add NOT NULL | `ALTER COLUMN ... SET NOT NULL` |
| Remove NOT NULL | `ALTER COLUMN ... DROP NOT NULL` |
| Create UNIQUE | Add `UNIQUE` after the column definition |
| Add UNIQUE | `ADD CONSTRAINT ... UNIQUE (...)` |
| `ADD CONSTRAINT` | Common pattern for adding constraints to existing tables |

# 💡 Memory Aid

**NOT NULL** 🚫❓ → **No missing values**

**UNIQUE** 1️⃣ → **No duplicates**

### 🔄 Constraint Syntax

**Create table:**

`column data_type NOT NULL`

`column data_type UNIQUE`

**Modify existing table:**

`ALTER COLUMN ... SET NOT NULL`

`ALTER COLUMN ... DROP NOT NULL`

`ADD CONSTRAINT ... UNIQUE (...)`
