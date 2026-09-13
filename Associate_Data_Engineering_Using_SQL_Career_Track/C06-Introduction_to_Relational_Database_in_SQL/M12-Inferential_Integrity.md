# 🛡️ Referential Integrity

## 1. 🔗 What Is Referential Integrity?

**Referential integrity** is an important database concept that ensures a record referencing another record in another table always refers to an **existing record**.

### 📌 Basic Rule

If:

`Table A → Table B`

then a record in **Table A** cannot point to a record in **Table B** that does not exist.

### 💡 Example

`professors.university_shortname → universities.id`

A professor's foreign key value must refer to an existing university.

---

# 2. 🔑 Referential Integrity and Foreign Keys

Referential integrity is a constraint involving **two tables**.

It is enforced through a **foreign key**.

### Example

If `professors` contains a foreign key referencing `universities`:

`professors → universities`

then referential integrity is maintained from:

**`professors` to `universities`**.

---

# 3. ⚠️ Referential Integrity Violations

Referential integrity can be violated in **two main ways**.

## 1️⃣ Delete Violation

Suppose:

`Table A → Table B`

If a record in **Table B** is already referenced by Table A and you try to delete it, the relationship can become invalid.

### Example

`Professor A → University X`

If `University X` is deleted while `Professor A` still references it:

❌ Referential integrity violation

---

## 2️⃣ Insert Violation

If you insert a record into **Table A** that references a record that does not exist in **Table B**, referential integrity is violated.

### Example

The `universities` table contains:

`EPF`

But you try to insert:

`professor.university_shortname = 'XYZ'`

when:

`XYZ`

does not exist in `universities`.

❌ Referential integrity violation

---

# 4. 🛡️ Why Foreign Keys Matter

Foreign keys help prevent these violations.

They can:

✅ Stop invalid references  
✅ Prevent accidental deletion of referenced records  
✅ Preserve relationships between tables

When an invalid operation is attempted, the database can **throw an error**.

---

# 5. 🗑️ `ON DELETE`

A foreign key can specify what should happen when a referenced record is deleted.

### Default Behavior

The default is:

`ON DELETE NO ACTION`

This means that if a referenced record is still being used, the database will **prevent the deletion** by throwing an error.

---

# 6. 🚫 `ON DELETE NO ACTION`

### Example

FOREIGN KEY (university_id)
REFERENCES universities(id)
ON DELETE NO ACTION

### Behavior

If:

`professors.university_id → universities.id`

and the university is still referenced:

`DELETE university`

❌ Error

The referenced university cannot be deleted while the foreign-key relationship would become invalid.

---

# 7. 🌊 `ON DELETE CASCADE`

`CASCADE` automatically propagates the deletion.

### Example

FOREIGN KEY (university_id)
REFERENCES universities(id)
ON DELETE CASCADE

### Behavior

If a referenced record in Table B is deleted:

1. The record in Table B is deleted.
2. All referencing records in Table A are automatically deleted.

### 💡 Example

`University X`

⬇️ referenced by

`Professor A`  
`Professor B`

Delete:

`University X`

Then:

`Professor A` → deleted  
`Professor B` → deleted

The deletion is **cascaded**.

---

# 8. 🚧 `ON DELETE RESTRICT`

`RESTRICT` is **almost identical** to `NO ACTION`.

Both prevent deletion when the referenced record is still being referenced.

### 📌 Difference

The differences are technical and beyond the scope of this course.

### 💡 For This Course

Think of:

`NO ACTION ≈ RESTRICT`

---

# 9. 🔄 `ON DELETE SET NULL`

`SET NULL` changes the foreign key value to:

`NULL`

when the referenced record is deleted.

### Example

Before deletion:

| professor | university_id |
|---|---|
| Professor A | EPF |

Delete the referenced university.

After:

| professor | university_id |
|---|---|
| Professor A | NULL |

### 💡 Key Idea

**Referenced record deleted → Foreign key becomes `NULL`**

---

# 10. ⚙️ `ON DELETE SET DEFAULT`

`SET DEFAULT` changes the foreign key to the column's **default value** when the referenced record is deleted.

### ⚠️ Requirement

This option only works if the foreign-key column has a **default value** specified.

### 💡 Key Idea

**Referenced record deleted → Foreign key becomes the column's default value**

---

# 11. 🔄 `ON DELETE` Behavior Comparison

| Option | What Happens When Referenced Record Is Deleted? |
|---|---|
| `NO ACTION` | Prevents deletion and throws an error |
| `RESTRICT` | Almost the same as `NO ACTION` |
| `CASCADE` | Deletes all referencing records automatically |
| `SET NULL` | Sets the foreign key to `NULL` |
| `SET DEFAULT` | Sets the foreign key to its default value |

---

# 🧠 Example: Professor → University

### Tables

**`universities`**

| id |
|---|
| EPF |
| UBE |

**`professors`**

| professor | university_id |
|---|---|
| Professor A | EPF |
| Professor B | EPF |
| Professor C | UBE |

### Relationship

`professors.university_id → universities.id`

### With `CASCADE`

Delete:

`EPF`

Result:

| professor | university_id |
|---|---|
| Professor C | UBE |

Professor A and Professor B are automatically deleted.

### With `SET NULL`

Delete:

`EPF`

Result:

| professor | university_id |
|---|---|
| Professor A | NULL |
| Professor B | NULL |
| Professor C | UBE |

---

# 🧠 Exam Key Points

| Concept | Key Point |
|---|---|
| **Referential Integrity** | A reference must always point to an existing record |
| **Foreign Key** | Enforces referential integrity between two tables |
| **Insert Violation** | Referencing a record that does not exist |
| **Delete Violation** | Deleting a referenced record while references still exist |
| `ON DELETE NO ACTION` | Prevents deletion when references exist |
| `ON DELETE RESTRICT` | Almost identical to `NO ACTION` |
| `ON DELETE CASCADE` | Deletes referencing records automatically |
| `ON DELETE SET NULL` | Changes referencing foreign keys to `NULL` |
| `ON DELETE SET DEFAULT` | Changes referencing foreign keys to their default value |
| `SET NULL` requirement | Foreign-key column must allow `NULL` |
| `SET DEFAULT` requirement | A default value must be defined |

# 💡 Memory Aid

### Referential Integrity 🔗

**Foreign Key → Must Point to Existing Record** ✅

### `ON DELETE`

`NO ACTION` 🚫 → **Don't delete**

`RESTRICT` 🚧 → **Restrict deletion**

`CASCADE` 🌊 → **Delete related records**

`SET NULL` ❓ → **Set FK to NULL**

`SET DEFAULT` ⚙️ → **Use default value**

### Core Rule

**Table A references Table B → Table A must not contain an invalid reference to Table B.**
