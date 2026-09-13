# 🔑 Keys and Superkeys

## 1. 🗝️ Key Constraints

**Key constraints** are an important concept in database systems.

They help identify records uniquely within database tables.

---

# 2. 📊 Database Model with Primary Keys

The previous chapter focused on **attribute constraints**, including:

- Data types
- `NOT NULL`
- `UNIQUE`

These constraints improved data quality but did **not change the overall structure of the database model**.

In this chapter, **primary keys** will be added.

### 🔑 Primary Keys in the Database

Three tables will receive primary keys:

- `professors`
- `organizations`
- `universities`

The primary keys will be named:

`id`

### 📌 Structural Changes

**`professors`**

A new `id` attribute will be added.

**`organizations`**

An existing column will be modified.

**`universities`**

An existing column will be modified.

### 🧩 ERD Symbol

In an **entity-relationship diagram (ERD)**:

**Underlined attribute name = Key** 🔑

---

# 3. 🔍 What Is a Key?

A database table usually has an attribute, or a combination of attributes, whose values are **unique across the entire table**.

These attributes can uniquely identify a record.

### Example

Suppose a table contains:

`license_no`

If every record has a different license number, then:

`license_no`

can uniquely identify each record.

---

# 4. 🧩 Superkey

A **superkey** is an attribute or combination of attributes that uniquely identifies every record.

The combination of **all attributes** in a table is always a superkey when the table contains unique records.

### Example

Suppose a table contains these attributes:

- `make`
- `model`
- `year`
- `license_no`
- `serial_no`

The combination:

`make + model + year + license_no + serial_no`

is a **superkey** because it uniquely identifies every record.

---

# 5. ✂️ Removing Attributes from a Superkey

A superkey can contain more attributes than necessary.

If an attribute can be removed and the remaining attributes still uniquely identify every record, the remaining combination is **still a superkey**.

### Example

If:

`make + model + year + license_no + serial_no`

uniquely identifies all records, and removing:

`year`

still leaves unique records:

`make + model + license_no + serial_no`

is still a **superkey**.

---

# 6. 🎯 Minimal Superkey

A **minimal superkey** is a superkey where **no attribute can be removed without losing uniqueness**.

This is the actual concept of a **key**.

### 📌 Definition

**Key = Minimal Superkey**

A key must:

✅ Uniquely identify records  
✅ Contain no unnecessary attributes

---

# 7. 🚗 Example: Car Table

Consider a table containing six different cars.

Possible attributes include:

- `make`
- `model`
- `year`
- `license_no`
- `serial_no`

The combination of **all attributes** is a superkey.

Other combinations may also be superkeys if they still uniquely identify every record.

---

# 8. 🔑 Candidate Keys

In the car example, there are **four minimal superkeys**:

1. `license_no`
2. `serial_no`
3. `model`
4. `make + year`

These are called **candidate keys**.

### Why?

Each one:

- Uniquely identifies every record
- Cannot have an attribute removed without losing uniqueness

---

# 9. 🧠 Why Are They Called Candidate Keys?

There may be **multiple candidate keys** in a table.

However, only **one key** can ultimately be chosen for the table.

Therefore, the minimal superkeys are called **candidate keys** because they are candidates for becoming the table's key.

---

# 10. 🔄 Superkey vs Candidate Key

| Concept | Meaning |
|---|---|
| **Superkey** | Attribute(s) that uniquely identify records |
| **Minimal Superkey** | Superkey with no unnecessary attributes |
| **Key** | A minimal superkey |
| **Candidate Key** | A minimal superkey that can be chosen as the table's key |
| **Primary Key** | The chosen key for the table |

### 💡 Memory Aid

**Superkey** → Unique ✅

**Minimal Superkey** → Unique + No Extra Attributes 🎯

**Candidate Key** → Potential key 🔑

**Primary Key** → Chosen key 🏆

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Key Constraint** | Helps uniquely identify records |
| **Superkey** | Attribute(s) that uniquely identify a record |
| **Minimal Superkey** | A superkey where no attribute can be removed without losing uniqueness |
| **Key** | A minimal superkey |
| **Candidate Key** | A minimal superkey that can be selected as the table's key |
| **Primary Key** | The chosen key for the table |
| **Primary Key Attribute** | Shown underlined in an ERD |
| `id` | Name used for the new primary keys in the three tables |
| **Professor table** | Gets a new `id` attribute |
| **Organizations / Universities** | Existing columns are modified for the key structure |

# 💡 Final Memory Aid

**SUPERKEY** 🔑  
→ Any unique combination

**MINIMAL SUPERKEY** ✂️  
→ Unique + nothing unnecessary

**CANDIDATE KEY** 🎯  
→ Possible key

**PRIMARY KEY** 🏆  
→ The chosen candidate key
