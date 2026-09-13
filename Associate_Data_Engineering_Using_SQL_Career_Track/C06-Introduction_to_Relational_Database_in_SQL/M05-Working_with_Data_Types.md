# 🧩 Working with Data Types

## 1. 📊 Data Types in PostgreSQL

Working with data types is straightforward in a database management system such as **PostgreSQL**.

Data types are an important part of database structure because they control:

- What values can be stored
- What form those values can take
- What operations can be performed on those values

---

# 2. 🛡️ Data Types as Attribute Constraints

Data types are **attribute constraints** and are applied to individual columns.

They define the **domain of values** for a column.

### 📌 Domain

The domain describes:

- What values are allowed ✅
- What values are not allowed ❌

### Example

A street number should contain an actual number.

A postal code should contain no more than **6 digits**, according to the defined convention.

### 🎯 Benefits

Data types help enforce:

- Consistent storage
- Valid values
- Consistent operations
- Better data quality

### 💡 Key Idea

**Data Type = Defines what a column can store and what can be done with its values.**

---

# 3. 🔤 Common PostgreSQL Data Types

PostgreSQL provides many data types.

These types are PostgreSQL-specific implementations, but many also appear in other database management systems and mostly conform to the SQL standard.

| Data Type | Purpose |
|---|---|
| `TEXT` | Stores character strings of any length |
| `VARCHAR` | Stores strings with a maximum number of characters |
| `CHAR` | Stores fixed-length character strings |
| `BOOLEAN` | Stores Boolean values such as `TRUE` / `FALSE` and also allows `NULL` |
| `DATE` | Stores dates |
| Date/Time types | Used for date and time calculations, including timezone support |
| `NUMERIC` | Stores numbers with arbitrary precision |
| `INTEGER` | Stores whole numbers within a certain range |
| `BIGINT` | Stores larger whole numbers than `INTEGER` |

---

# 4. 🔤 `TEXT`, `VARCHAR`, and `CHAR`

### `TEXT`

Allows character strings of **any length**.

Example:

`TEXT`

### `VARCHAR`

Specifies a **maximum number of characters**.

Example:

`VARCHAR(64)`

### `CHAR`

Specifies a **fixed-length character string**.

Example:

`CHAR(5)`

### 💡 Memory Aid

`TEXT` → Any length 📝  
`VARCHAR(n)` → Maximum length 🔢  
`CHAR(n)` → Fixed length 📏

---

# 5. ✅ `BOOLEAN`

The `BOOLEAN` type represents logical values.

Examples:

`TRUE`

`FALSE`

It can also represent an unknown value using:

`NULL`

### 💡 Example

A student's tuition payment status can be stored as:

`TRUE` → Paid ✅

`FALSE` → Not paid ❌

`NULL` → Unknown ❓

---

# 6. 📅 Date and Time Types

PostgreSQL provides different types for:

- Dates
- Times
- Date and time calculations
- Timezone-supported values

A birth date, for example, can naturally be stored as:

`DATE`

---

# 7. 🔢 Numeric Data Types

### `NUMERIC`

Used for numbers with **arbitrary precision**.

### `INTEGER`

Stores **whole numbers** within a certain range.

### `BIGINT`

Used when the number is too large for the `INTEGER` range.

### 💡 Memory Aid

`INTEGER` → Whole numbers 🔢

`BIGINT` → Larger whole numbers 🔢⬆️

`NUMERIC` → Precise/general numerical values 🎯

---

# 8. 🏗️ Specifying Types When Creating a Table

Data types are specified when defining table columns.

### Example

Suppose we create a student table containing:

- Social security number
- Name
- Date of birth
- Average grade
- Tuition payment status

A possible structure is:

CREATE TABLE students (
    ssn INTEGER,
    name VARCHAR(64),
    dob DATE,
    average_grade NUMERIC(3,2),
    tuition_paid BOOLEAN
);

### 📌 Column Breakdown

| Column | Data Type | Meaning |
|---|---|---|
| `ssn` | `INTEGER` | Whole-number social security number |
| `name` | `VARCHAR(64)` | String with a maximum of 64 characters |
| `dob` | `DATE` | Date of birth |
| `average_grade` | `NUMERIC(3,2)` | Maximum 3 total digits, with 2 digits after the decimal |
| `tuition_paid` | `BOOLEAN` | True/false tuition payment status |

---

# 9. 🎯 `NUMERIC(3,2)`

`NUMERIC(3,2)` means:

- **Precision = 3** → Total number of digits
- **Scale = 2** → Number of digits after the decimal point

Therefore, the value can contain:

**3 total digits**

with:

**2 digits after the decimal point**

### Example

`9.99` ✅

---

# 10. 🔄 Altering a Data Type

Data types can also be changed **after a table has been created**.

Use:

`ALTER TABLE`

together with:

`ALTER COLUMN`

### 🧩 Syntax

ALTER TABLE table_name
ALTER COLUMN column_name TYPE new_data_type;

### Example

To increase the maximum name length from 64 to 128 characters:

ALTER TABLE students
ALTER COLUMN name TYPE VARCHAR(128);

---

# 11. 🛠️ Using `USING` When Changing Types

Sometimes existing values must be **transformed** before they can fit the new data type.

In this case, use the:

`USING`

keyword.

### 🧩 Pattern

ALTER TABLE table_name
ALTER COLUMN column_name TYPE new_data_type
USING transformation;

### Example

Suppose:

`average_grade`

needs to be changed to:

`INTEGER`

PostgreSQL would normally keep the portion before the fractional point.

Using `USING`, we can instead specify a transformation such as rounding to the nearest integer.

Example pattern:

ALTER TABLE students
ALTER COLUMN average_grade TYPE INTEGER
USING ROUND(average_grade);

### 💡 Key Idea

`USING` = **Transform existing values before changing the column type** 🔄

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Data Type** | Defines the allowed form/domain of values in a column |
| **Attribute Constraint** | Constraint applied to an individual column |
| `TEXT` | Strings of any length |
| `VARCHAR(n)` | Strings with a maximum length |
| `CHAR(n)` | Fixed-length character strings |
| `BOOLEAN` | Boolean values plus `NULL` |
| `DATE` | Stores dates |
| `NUMERIC` | Numbers with arbitrary precision |
| `INTEGER` | Whole numbers in a certain range |
| `BIGINT` | Larger whole numbers |
| `NUMERIC(3,2)` | 3 total digits, 2 after the decimal |
| `ALTER TABLE` | Changes an existing table |
| `ALTER COLUMN` | Changes a column definition |
| `TYPE` | Specifies the new data type |
| `USING` | Specifies a transformation before changing a data type |

# 💡 Memory Aid

**Data Types = Column Rules** 🛡️

`TEXT` → Any-length text 📝  
`VARCHAR` → Maximum-length text 📏  
`CHAR` → Fixed-length text 📐  
`BOOLEAN` → True / False / NULL ✅❌❓  
`DATE` → Dates 📅  
`NUMERIC` → Precise numbers 🎯  
`INTEGER` → Whole numbers 🔢  
`BIGINT` → Larger whole numbers 🔢⬆️

**Change a Type:**

`ALTER TABLE → ALTER COLUMN → TYPE`

**Need to transform existing values first?**

`USING` 🔄
