# Defining Relationships Between Tables 🔗

## Overview 📚

Tables in a relational database can have different types of relationships.

The three relationship types covered in this lesson are:

- **One-to-many**
- **One-to-one**
- **Many-to-many**

# 1. One-to-Many Relationship 1️⃣➡️🔢

A **one-to-many relationship** occurs when **one entity can be associated with multiple entities**, while each of those related entities is associated with only one entity on the other side.

> **One → Many**

This is the **most common type of relationship**.

### Examples

- One artist → Many songs
- One author → Many books
- One director → Many movie titles

### Example: Authors and Books 📚

**Jane Austen** wrote many books, but each book has only one author.

The relationship is:

**One Author → Many Books**

The `books` table can be connected to the `authors` table using:

`author_id`

### Key Idea

The same `author_id` can appear in multiple records in the `books` table because one author can have many books.

# 2. One-to-One Relationship 1️⃣↔️1️⃣

A **one-to-one relationship** occurs when each entity is associated with **exactly one corresponding entity**.

> **One → One**

One-to-one relationships imply **unique pairings** and are less common.

### Example: Fingerprints and People 🧑‍💼

A fingerprint can be associated with one person, creating a one-to-one relationship between:

- A person
- A set of fingerprints

### Airport Border Control Example ✈️

A database might contain:

- `individuals` table
- `fingerprints` table

The records can be connected using:

`passport_number`

Conceptually:

**One Individual Record → One Fingerprint Record**

### Important Distinction ⚠️

An individual may have **four fingerprints**, but this does **not automatically make it a one-to-many relationship**.

In the example:

- One individual = one record in the `individuals` table.
- One set of fingerprints = one record in the `fingerprints` table.
- The four fingerprints are stored as **four different fields within that one fingerprint record**.

Therefore:

**One Individual Record → One Fingerprint Record**

= **One-to-one relationship**

### Key Idea

The relationship is determined by the **records/entities being related**, not simply by counting individual values contained within a record.

# 3. Many-to-Many Relationship 🔢↔️🔢

A **many-to-many relationship** occurs when:

- One entity can be associated with many entities.
- Each of those entities can also be associated with many entities.

> **Many ↔ Many**

### Example: Languages and Countries 🌍🗣️

Languages and countries can have a many-to-many relationship.

For example:

**Belgium → French, German, Dutch**

Belgium has multiple official languages.

At the same time:

**Dutch → Netherlands + Belgium**

Dutch is an official language in multiple countries.

Therefore:

**Many Countries ↔ Many Languages**

# 4. Relationship Comparison 📊

| Relationship | Meaning | Example |
|---|---|---|
| **One-to-Many** | One entity is associated with many entities | One author → Many books |
| **One-to-One** | One entity is associated with one corresponding entity | One individual → One fingerprint record |
| **Many-to-Many** | Many entities can be associated with many entities | Many countries ↔ Many languages |

# 5. One-to-Many Example 🔗

### Authors

| author_id | author |
|---:|---|
| 1 | Jane Austen |
| 2 | Mark Twain |

### Books

| book_id | title | author_id |
|---:|---|---:|
| 101 | Book A | 1 |
| 102 | Book B | 1 |
| 103 | Book C | 2 |

Relationship:

**Jane Austen → Book A + Book B**

**Mark Twain → Book C**

The `author_id` connects the books to their authors.

# 6. One-to-One Example 🔗

### Individuals

| passport_number | name |
|---|---|
| P001 | Person A |
| P002 | Person B |

### Fingerprints

| passport_number | fingerprint_data |
|---|---|
| P001 | Fingerprint Set A |
| P002 | Fingerprint Set B |

Relationship:

**One Individual → One Fingerprint Record**

The `passport_number` connects the records.

# 7. Many-to-Many Example 🔗

### Countries and Languages

A country can have multiple official languages:

**Belgium → French, German, Dutch**

A language can belong to multiple countries:

**Dutch → Belgium, Netherlands**

Therefore:

**Countries ↔ Languages**

is a many-to-many relationship.

# 8. How to Identify the Relationship 🧠

Ask two questions:

### Question 1

**How many records on the other side can one record be associated with?**

### Question 2

**How many records on this side can one record be associated with?**

### Results

**One + One**

→ One-to-one

**One + Many**

→ One-to-many

**Many + Many**

→ Many-to-many

# Exam / Interview Key Points 🎯

- There are three relationship types covered:
  - **One-to-one**
  - **One-to-many**
  - **Many-to-many**
- **One-to-many** is the most common relationship type.
- One-to-many means one entity can be associated with several entities.
- Examples:
  - One artist → Many songs
  - One author → Many books
  - One director → Many movie titles
- In the authors/books example, `author_id` connects books to authors.
- **One-to-one** means entities have unique pairings.
- One-to-one relationships are less common.
- In the fingerprint example, one individual record corresponds to one fingerprint record.
- Having four fingerprints stored as four fields in one record does **not** make the relationship one-to-many.
- **Many-to-many** means many entities on one side can relate to many entities on the other side.
- Languages and countries are an example of many-to-many.
- Belgium has multiple official languages.
- Dutch can be an official language in multiple countries.

# Quick Memory Aid 🚀

**One-to-One = 1 ↔ 1**

**One-to-Many = 1 → Many**

**Many-to-Many = Many ↔ Many**

### Examples

**Author → Books** = One-to-many 📚

**Individual → Fingerprint Record** = One-to-one 🧑‍💼

**Countries ↔ Languages** = Many-to-many 🌍

# Most Important Concept ⭐

> **A one-to-many relationship connects one entity to multiple entities, a one-to-one relationship connects one entity to one corresponding entity, and a many-to-many relationship allows multiple entities on both sides to be associated with one another. The relationship is determined by how records/entities are related, not simply by how many values are stored within an individual record.**
