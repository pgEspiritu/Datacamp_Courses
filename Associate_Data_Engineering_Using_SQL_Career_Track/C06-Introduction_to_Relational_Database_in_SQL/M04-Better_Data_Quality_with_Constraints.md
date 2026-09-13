# 🛡️ Better Data Quality with Constraints

## 1. 📐 What Are Integrity Constraints?

A database is more than just a collection of tables.

A database pushes data into a **pre-defined structure** or **model** by enforcing:

- Data types
- Relationships
- Other rules

These rules are generally called **integrity constraints**.

### 🎯 Purpose

Integrity constraints help ensure that data follows the structure and rules defined by the database.

---

# 2. 🧩 Types of Integrity Constraints

Integrity constraints can be divided into **three main types**:

| Constraint Type | Purpose | Covered In |
|---|---|---|
| **Attribute Constraints** | Define rules for individual columns, such as data types | This chapter |
| **Key Constraints** | Uniquely identify records using keys such as primary keys | Next chapter |
| **Referential Integrity Constraints** | Connect and maintain relationships between tables | Final chapter |

### 💡 Memory Aid

**Attribute → Column rules** 📊  
**Key → Record identity** 🔑  
**Referential → Table relationships** 🔗

---

# 3. 📊 Attribute Constraints

An **attribute constraint** applies rules to a database column.

The simplest example is specifying a **data type**.

### Example

If a column uses an integer data type:

`age INTEGER`

only integer values can be stored in that column.

This helps enforce a consistent structure for the data.

---

# 4. 🎯 Why Use Constraints?

Constraints help **push data into a certain form**.

For example, if users enter birthdates, constraints can help ensure that the values follow the same expected structure.

### ✅ Benefits

Constraints provide:

- **Consistency**
- **Data quality**
- **Standardized data structure**
- Less tedious **pre-processing** of human-entered data

### 📌 Key Idea

Without constraints:

`Human input → Different forms → More cleaning`

With constraints:

`Human input → Database rules → More consistent data` ✅

Database management systems can enforce these rules automatically.

---

# 5. 🧱 Data Types as Attribute Constraints

In PostgreSQL, a column can be assigned a specific **data type**.

Examples of PostgreSQL data types include:

| Data Type | Purpose |
|---|---|
| `bigint` | Stores large integer values |
| `character varying` | Stores strings of characters |
| `cidr` | Stores IP network addresses |

### 🌐 Example: `cidr`

A column using `cidr` expects values that fit the structure of an IP network address.

Therefore, values that do not fit the required structure are not allowed.

---

# 6. ⚠️ Data Types Restrict SQL Operations

Data types do not only control what can be stored.

They also affect which **SQL operations** can be performed.

For example, PostgreSQL cannot directly calculate a product between:

`integer × text`

Even if the text column contains numbers.

### Example

Suppose:

`wind_speed` = text

Even if the value looks like:

`20`

PostgreSQL still treats it as **text**, not a number.

Therefore:

`integer * wind_speed`

cannot be performed directly.

---

# 7. 🔄 Type Casting

The solution is **type casting**.

A **type cast** converts a value from one data type to another.

The conversion can happen **on the fly**, immediately before an operation.

### 🧩 `CAST()` Syntax

CAST(column_name AS data_type)

### Example

CAST(wind_speed AS INTEGER)

This converts `wind_speed` from text to an integer.

It can then be used in a calculation.

### 💡 Pattern

`CAST(value AS desired_data_type)`

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Integrity Constraint** | Rule that helps enforce a database's defined structure |
| **Attribute Constraint** | Constraint applied to an attribute/column |
| **Data Type** | Defines what kind of data a column can store |
| **Key Constraint** | Uses keys such as primary keys to uniquely identify records |
| **Referential Integrity** | Maintains relationships between tables |
| `bigint` | PostgreSQL integer data type for large integer values |
| `character varying` | PostgreSQL string data type |
| `cidr` | PostgreSQL data type for IP network addresses |
| **Type Cast** | Converts a value from one data type to another |
| `CAST()` | Performs an explicit type conversion |
| `AS` in `CAST()` | Specifies the desired target data type |

# 💡 Memory Aid

**Constraints = Rules for Data Quality** 🛡️

**Attribute Constraints → What goes inside a column** 📊

**Key Constraints → Who/what uniquely identifies a row** 🔑

**Referential Integrity → How tables stay connected** 🔗

**`CAST()` → Convert Data Type** 🔄
