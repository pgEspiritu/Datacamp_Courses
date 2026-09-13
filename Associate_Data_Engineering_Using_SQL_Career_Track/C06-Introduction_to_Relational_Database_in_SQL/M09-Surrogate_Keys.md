# 🆔 Surrogate Keys

## 1. 🧩 What Is a Surrogate Key?

A **surrogate key** is an **artificial primary key**.

It is not based on a native column in the original data.

Instead, it is a column that exists specifically to provide a **primary key**.

### 💡 Key Idea

**Surrogate Key = Artificial Primary Key** 🆔

---

# 2. 🎯 Why Use a Surrogate Key?

There are several reasons to create a surrogate key.

### ✅ 1. Keep the Primary Key Small

A primary key should ideally consist of **as few columns as possible**.

A surrogate key can be a single column instead of using multiple existing columns.

### ✅ 2. Keep the Primary Key Stable

A primary key should **never change over time**.

Other attributes may change.

For example:

`color` → may change if a car is repainted 🎨

But an artificial ID can remain the same:

`id = 101`

### 💡 Key Idea

**Other attributes can change, but the surrogate primary key should remain the same for the record.**

---

# 3. 🚗 Example: Car Table

Suppose we have:

| license_no | make | model | color |
|---|---|---|---|
| ABC123 | Toyota | Corolla | Red |
| DEF456 | Honda | Civic | Blue |

The `license_no` column is a good primary key because the license number is unlikely to change.

The `color` column is **not** suitable because it can change.

### ✅ No Surrogate Key Needed

`license_no`

already provides a suitable single-column primary key.

---

# 4. 🔑 When a Surrogate Key Helps

Suppose the table only contains:

| make | model |
|---|---|
| Toyota | Corolla |
| Honda | Civic |
| Ford | Focus |

The sensible primary key would be:

`make + model`

This requires **two columns**.

A surrogate key can simplify this by adding:

`id`

### Result

| id | make | model |
|---:|---|---|
| 1 | Toyota | Corolla |
| 2 | Honda | Civic |
| 3 | Ford | Focus |

Now:

`id`

can uniquely identify each record.

---

# 5. 🔢 Surrogate Key with `SERIAL`

PostgreSQL provides the:

`SERIAL`

data type for creating **auto-incrementing numbers**.

### Example

CREATE TABLE cars (
    id SERIAL PRIMARY KEY,
    make VARCHAR(50),
    model VARCHAR(50)
);

### 🔄 How It Works

When a column uses `SERIAL`:

- Existing records receive numbers.
- New records automatically receive a number.
- The new number does not already exist.

Example:

| id | make | model |
|---:|---|---|
| 1 | Toyota | Corolla |
| 2 | Honda | Civic |
| 3 | Ford | Focus |

When a new record is inserted:

`id = 4`

is automatically assigned.

---

# 6. 🚫 Duplicate ID

If you try to manually insert an ID that already exists, the **primary key constraint** prevents the duplicate.

Example:

Existing:

`id = 1`

Attempting to insert another:

`id = 1`

❌ Not allowed because the primary key must remain unique.

### 💡 Key Idea

The `id` column:

✅ Uniquely identifies each record  
✅ Can be referenced by other tables  
✅ Prevents duplicate primary-key values

---

# 7. 🧱 Another Surrogate Key Strategy

A surrogate key does not have to be an auto-incrementing number.

Another approach is to create a new column by **combining existing columns**.

### Step 1️⃣ Add a new column

Add a column using:

`VARCHAR`

### Step 2️⃣ Update the column

Populate it by concatenating existing values.

### Step 3️⃣ Use `CONCAT()`

The `CONCAT()` function combines values from two or more columns.

### Example

UPDATE table_name
SET new_id = CONCAT(column1, column2);

### Step 4️⃣ Use the New Column as the Primary Key

The newly created column can then be turned into a **surrogate primary key**.

---

# 8. 🧩 `CONCAT()`

`CONCAT()` **glues together** values from multiple columns.

### 🧩 Syntax

CONCAT(column1, column2)

### Example

CONCAT(firstname, lastname)

This combines:

`firstname + lastname`

into one value.

---

# 9. 👨‍🏫 Surrogate Key in the `professors` Table

In the course database, a surrogate key is added to:

`professors`

### Why?

The existing attributes are not completely suitable as a primary key.

There could theoretically be:

**More than one professor with the same name working for the same university.**

This could result in duplicate combinations.

### ✅ Solution

Add an auto-incrementing:

`id`

column.

This ensures that each professor can be uniquely referenced.

---

# 10. 🏢 Why Organizations and Universities Do Not Need One

Surrogate keys are not necessary for:

- `organizations`
- `universities`

because their names can be assumed to be **unique** in this database.

### Organizations

It is unlikely that two organizations have exactly the same name, partly because of trademark considerations.

### Universities

The same assumption is made for universities.

Therefore, their existing names can serve as suitable identifiers.

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Surrogate Key** | Artificial primary key not based on a native data column |
| **Purpose** | Provides a simple and stable unique identifier |
| **Primary Key Size** | Ideally uses as few columns as possible |
| **Primary Key Stability** | Should not change over time |
| `SERIAL` | PostgreSQL data type for auto-incrementing numbers |
| `id` | Common surrogate key column |
| **Auto-increment** | New records automatically receive a new number |
| `CONCAT()` | Combines values from two or more columns |
| `VARCHAR` surrogate key | Can be created by combining existing column values |
| `UPDATE` | Used to populate the newly created surrogate-key column |
| `professors` | Uses a surrogate key because existing attributes may not uniquely identify every professor |
| `organizations` | Existing names can be assumed unique |
| `universities` | Existing names can be assumed unique |

# 🔄 Surrogate Key Workflow

### Numeric Surrogate Key

`Add id column` → `SERIAL` → `PRIMARY KEY` → `Auto-increment` 🆔

### Combined-Column Surrogate Key

`Add VARCHAR column` → `UPDATE` → `CONCAT()` → `PRIMARY KEY` 🔗

# 💡 Memory Aid

**Surrogate Key = Artificial + Unique + Stable** 🆔

`SERIAL` → Auto-number 🔢

`CONCAT()` → Combine columns 🔗

`id` → Simple record identifier 🎯

**Professors → Surrogate key needed** 👨‍🏫  
**Organizations → Existing name** 🏢  
**Universities → Existing name** 🏫
