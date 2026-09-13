# 🔗 Model More Complex Relationships

## 1. 🧩 From 1:N to More Complex Relationships

Previously, a **1:N relationship** was modeled between:

`professors` 👨‍🏫  
and  
`universities` 🏫

Now we move to a more complex relationship:

`professors` 👨‍🏫 ↔ `organizations` 🏢

---

# 2. 🔢 1:N Relationship: Professors and Universities

A professor can work for **at most one university**.

A university can have **many professors**.

Therefore:

**University → Professors = 1:N**

### 📌 Foreign Key Rule

For a 1:N relationship, the foreign key is placed in the table representing the entity that can have **at most one associated entity**.

Here:

`professors`

contains:

`university_shortname`

which references:

`universities.id`

### 💡 Memory Aid

**1:N → Foreign key goes on the N-side.** 🔑

---

# 3. 🔄 Professors and Organizations

The relationship between `professors` and `organizations` is different.

A professor can have:

- More than one organization affiliation

An organization can have:

- More than one professor affiliated with it

### Example

One professor:

`Professor A`

can be:

- Chairman of a bank
- President of a golf club

At the same time, one organization can have several professors.

Therefore, this is an:

**N:M relationship**

Also written as:

**Many-to-Many**

---

# 4. 🔷 N:M Relationship

An **N:M relationship** means:

`Many professors ↔ Many organizations`

### 📌 Example

**Professors**

| Professor | Organizations |
|---|---|
| Professor A | Bank |
| Professor A | Golf Club |
| Professor B | Bank |

The same professor can appear with multiple organizations.

The same organization can also appear with multiple professors.

---

# 5. 🆕 Relationship Attribute: `function`

The relationship itself has an attribute:

`function`

This describes the professor's role in the organization.

### Example

| Professor | Organization | Function |
|---|---|---|
| Professor A | Bank | Chairman |
| Professor A | Golf Club | President |

### 💡 Important

`function` belongs to the **relationship**, not simply to the professor or organization.

---

# 6. 🗑️ The `affiliations` Entity Type

In the final database model, the original **`affiliations` entity type disappears**.

However, the database still contains **four tables**:

1. `professors`
2. `universities`
3. `organizations`
4. A table representing the **N:M relationship** between professors and organizations

The fourth table is used to implement the relationship.

---

# 7. 🏗️ Implementing an N:M Relationship

An N:M relationship is implemented using an **ordinary database table**.

This relationship table contains:

- A foreign key to `professors`
- A foreign key to `organizations`
- Any attributes belonging to the relationship

### Structure

`professor_id` → `professors.id`

`organization_id` → `organizations.id`

`function` → role in the organization

---

# 8. 🔑 Foreign Keys in the Relationship Table

The relationship table contains **two foreign keys**.

### Professor Foreign Key

`professor_id`

references:

`professors.id`

### Organization Foreign Key

`organization_id`

references:

`organizations.id`

### Relationship

`professor_id → professors.id`

`organization_id → organizations.id`

---

# 9. 🧱 Data Types of the Foreign Keys

The foreign key data types must conform to the referenced primary keys.

### `professor_id`

The primary key:

`professors.id`

uses:

`serial`

which is an integer type.

Therefore:

`professor_id`

uses:

`integer`

### `organization_id`

The primary key in `organizations` uses:

`varchar(256)`

Therefore:

`organization_id`

uses:

`varchar(256)`

### 💡 Key Rule

**Foreign Key Data Type = Referenced Primary Key Data Type** 🔗

---

# 10. 📋 Example Relationship Table

A relationship table could look like:

| professor_id | organization_id | function |
|---:|---|---|
| 1 | Bank001 | Chairman |
| 1 | Golf001 | President |
| 2 | Bank001 | Director |

This table represents the relationships between professors and organizations.

---

# 11. ⚠️ Why No Primary Key?

In this example, **no primary key is defined** for the relationship table.

Why?

A professor can theoretically have **multiple functions in the same organization**.

For example:

| professor_id | organization_id | function |
|---:|---|---|
| 1 | Bank001 | Chairman |
| 1 | Bank001 | Director |

Therefore:

`professor_id + organization_id`

is not necessarily unique.

---

# 12. 🧩 Possible Composite Primary Key

It would technically be possible to use all three attributes:

`professor_id + organization_id + function`

as a primary key.

This would provide a form of uniqueness.

However, the lesson considers this:

**A bit over the top.**

Therefore, the example relationship table is created **without a primary key**.

---

# 13. 🔄 N:M Relationship Model

### Main Tables

**`professors`**

| id |
|---:|
| 1 |
| 2 |

**`organizations`**

| id |
|---|
| Bank001 |
| Golf001 |

### Relationship Table

**`affiliations`**

| professor_id | organization_id | function |
|---:|---|---|
| 1 | Bank001 | Chairman |
| 1 | Golf001 | President |
| 2 | Bank001 | Director |

### Relationship

`professors`  
⬇️  
`affiliations`  
⬆️  
`organizations`

The relationship table connects the two entities.

---

# 14. 🔄 Migrating Existing Affiliation Data

The course already has a **pre-populated `affiliations` table**.

Therefore, implementing the final N:M relationship is not as simple as creating an empty table.

The existing affiliation data must be:

1. Linked to the appropriate professors.
2. Linked to the appropriate organizations.
3. Migrated into the new relationship table.

### 🎯 Goal

Transform the existing affiliation data into a proper **N:M relationship table**.

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **1:N Relationship** | One entity can relate to many entities |
| **N:M Relationship** | Many entities can relate to many entities |
| **Professor → University** | 1:N relationship |
| **Professor ↔ Organization** | N:M relationship |
| **1:N Foreign Key** | Foreign key goes on the N-side |
| **N:M Implementation** | Use a separate relationship table |
| **Relationship Table** | Contains two foreign keys connecting the two entities |
| `professor_id` | Foreign key referencing `professors.id` |
| `organization_id` | Foreign key referencing `organizations.id` |
| `function` | Attribute belonging to the professor-organization relationship |
| **Foreign Key Type** | Must match the referenced primary key's type |
| `serial` | Type used by `professors.id`; `professor_id` therefore uses `integer` |
| `varchar(256)` | Type used by `organizations.id`; `organization_id` conforms to it |
| **Primary Key on relationship table** | Not defined in this example |
| **Why no PK?** | A professor can theoretically have multiple functions in one organization |
| **Composite PK possibility** | `professor_id + organization_id + function` could provide uniqueness |
| **Existing affiliations data** | Must be linked and migrated into the new relationship table |

# 💡 Memory Aid

### 1:N 🔢

**One University → Many Professors**

`universities.id`  
⬇️  
`professors.university_shortname`

### N:M 🔄

**Many Professors ↔ Many Organizations**

Use a **relationship table**:

`professor_id` 🔗 `organization_id`

plus:

`function`

### 🏆 Core Rule

**1:N → One foreign key on the N-side**

**N:M → Two foreign keys in a separate relationship table**
