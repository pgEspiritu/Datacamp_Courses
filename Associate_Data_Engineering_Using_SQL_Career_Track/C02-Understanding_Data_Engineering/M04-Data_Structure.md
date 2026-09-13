# Data Structures

## Overview

This chapter focuses on **data storage**. The first topic is understanding the three major types of data structures:

1. **Structured data**
2. **Semi-structured data**
3. **Unstructured data**

## 1. Structured Data

**Structured data** follows a rigid, predefined structure and is easy to search, organize, and analyze.

### Characteristics

- Organized into **rows and columns**.
- Each column has a defined data type.
- Follows a predefined schema/model.
- Easy to search and organize.
- Relationships between datasets can be established easily.
- Commonly stored in **relational databases**.
- Typically queried using **SQL (Structured Query Language)**.
- Approximately **20% of data is structured** according to the course.

### Example: Employee Table

A structured employee table may contain:

| Column | Example Data Type | Example |
|---|---|---|
| Index | Number | Unique ID |
| First Name | Text | Rick |
| Last Name | Text | Sanchez |
| Team | Text | Engineering |
| Role | Text | Developer |
| Part-Time | Boolean | `true` / `false` |

### Important Characteristics

- Each **row** represents an employee.
- Each **column** represents a specific attribute.
- Each column expects a particular data type.
- A numeric **index** can be used as a unique identifier because multiple employees may have the same name.
- A Boolean field can contain only **true or false**.

## 2. Relational Database

Structured tables can be connected to other structured tables using common fields.

Example:

**Employee Table → Office Table**

If both tables contain an **Office** column, they can be related using that field.

> Tables that can be connected through related fields form a **relational database**.

### Key Concept

**Structured data → Tables → Relationships → Relational Database → SQL**

## 3. Semi-Structured Data

**Semi-structured data** has some organization or structure but allows more flexibility than structured data.

### Characteristics

- Has a recognizable structure or model.
- More flexible than relational/structured data.
- Relatively easy to organize.
- Supports different types of data.
- Can be grouped to form relationships.
- Relationships are generally less straightforward than in relational databases.
- Commonly stored in **NoSQL databases**.
- Common formats include:
  - **JSON**
  - **XML**
  - **YAML**

### Flexibility

Semi-structured data allows structures that would be difficult to represent in a rigid relational table.

For example, different users can have different numbers of favorite artists.

### Example: JSON

A user record may contain:

- User ID
- First name
- Last name
- Favorite artists

One user might have:

- 4 favorite artists

Another might have:

- 2 favorite artists

Another might have:

- 3 favorite artists

This flexibility is possible because semi-structured formats do not require every record to have exactly the same number of values.

## 4. NoSQL

Semi-structured data is commonly stored in **NoSQL databases**.

> **SQL databases** generally use structured, relational data, while **NoSQL databases** commonly support more flexible data structures.

## 5. Unstructured Data

**Unstructured data** does not follow a predefined model and generally cannot be represented naturally as rows and columns.

### Characteristics

- No rigid schema.
- Difficult to search and organize.
- Does not fit naturally into traditional tables.
- Commonly includes:
  - Text
  - Audio
  - Images
  - Videos
- Frequently stored in **data lakes**.
- Can also exist in data warehouses or databases.
- Represents most of the data around us.

### Examples at Spotflix

- Song lyrics
- Songs/audio files
- Album pictures
- Artist profile pictures
- Music videos

### Value of Unstructured Data

Unstructured data can be extremely valuable, but its lack of structure makes it difficult to search, organize, and analyze.

The development of **machine learning and artificial intelligence** has made it increasingly possible to extract useful information and value from unstructured data.

## 6. Adding Structure to Unstructured Data

Unstructured data can be processed to add structure.

### Example: Music Analysis

Machine learning algorithms could analyze songs for:

- Song spectrum
- Beats per minute (BPM)
- Chord progressions
- Genres

This information can help categorize songs.

Another approach is to ask artists to provide additional information when uploading songs, such as:

- Genre
- Tags
- Other metadata

Adding this information makes the data more **semi-structured**, making it easier to search and organize.

## Comparison of the Three Data Types

| Feature | Structured | Semi-Structured | Unstructured |
|---|---|---|---|
| **Structure** | Rigid | Flexible | No predefined structure |
| **Schema** | Fixed | Flexible / partial | None or very limited |
| **Organization** | Easy | Relatively easy | Difficult |
| **Rows & Columns** | Yes | Not necessarily | No |
| **Typical Storage** | Relational databases | NoSQL databases | Data lakes |
| **Common Formats** | Tables | JSON, XML, YAML | Text, audio, images, video |
| **Querying** | SQL | NoSQL/query tools | Specialized tools/ML/AI |
| **Relationships** | Easy to establish | Possible but less straightforward | Difficult |

## Quick Examples

### Structured
**Employee table**

`Employee ID | Name | Team | Role | Salary`

### Semi-Structured
**JSON user profile**

`User ID → Name → Favorite Artists`

Different users can have different numbers of favorite artists.

### Unstructured
- Song
- Video
- Image
- Lyrics
- Audio recording

## Quick Memory Aid

**Structured = Strict**

- Fixed schema
- Rows and columns
- Relational databases
- SQL

**Semi-Structured = Flexible**

- Some structure
- Flexible schema
- JSON/XML/YAML
- NoSQL

**Unstructured = No fixed model**

- Text
- Audio
- Images
- Video
- Data lakes

## Exam / Interview Key Points

- **Structured data** follows a rigid schema and is typically organized into rows and columns.
- Structured data is commonly stored in **relational databases** and queried using **SQL**.
- Tables in a relational database can be connected using related fields.
- **Semi-structured data** provides structure while allowing greater flexibility.
- Common semi-structured formats are **JSON, XML, and YAML**.
- Semi-structured data is commonly associated with **NoSQL databases**.
- **Unstructured data** does not follow a predefined model and does not naturally fit into rows and columns.
- Common examples of unstructured data include **text, audio, images, and video**.
- Unstructured data is commonly stored in **data lakes**.
- Machine learning and AI can help extract value from unstructured data.
- Adding metadata such as **genre and tags** can make unstructured data more semi-structured.
- The key trade-off is:

**More structure → Easier organization and querying**

**More flexibility → Less rigid organization but more freedom in the data format**

## Core Comparison

**Structured:** Fixed structure → Relational database → SQL

**Semi-Structured:** Flexible structure → NoSQL → JSON/XML/YAML

**Unstructured:** No fixed structure → Data lake → ML/AI and specialized processing
