# Processing Data

## Overview

The third and final chapter focuses on **moving and processing data**.

Data processing is a key part of data engineering because raw data often needs to be transformed, cleaned, organized, and optimized before it can be effectively used for analysis.

## What Is Data Processing?

**Data processing** is the process of **converting raw data into meaningful information**.

Examples of data processing include:

- Moving data to a data lake.
- Splitting data into different tables.
- Removing corrupted files.
- Cleaning data.
- Transforming data formats.
- Extracting metadata.
- Organizing data according to a schema.
- Combining data.
- Validating data.
- Optimizing data for storage or retrieval.

## Why Process Data?

Data processing provides several important benefits.

### 1. Remove Unnecessary Data

Not all collected data needs to be kept permanently.

For example, when launching a new feature, an organization may collect many indicators to monitor whether it is working correctly. Once the feature becomes stable, some of this monitoring data may no longer be needed.

Removing unnecessary data helps reduce:

- Storage costs
- Processing costs
- Network costs

### 2. Reduce Data Size

Uncompressed data can be significantly larger than compressed data.

> Uncompressed data can be **10 times larger** than compressed data.

Processing and compressing data can therefore reduce:

- Storage requirements
- Processing requirements
- Network bandwidth
- Infrastructure costs

### 3. Convert Data to a More Useful Format

Data may be received in one format but be more useful in another format.

There can be a trade-off between:

- File size
- Quality
- Performance
- Cost

## Spotflix Audio Example

At Spotflix, artists may upload high-quality master files in:

- `.wav`
- `.flac`

These files provide high audio quality but are relatively large.

Streaming these large master files directly to users would increase network costs.

Spotflix therefore converts them into:

- `.ogg`

The `.ogg` files are:

- Smaller
- Better suited for streaming
- Slightly lower in sound quality
- Less expensive to transmit

### Processing Flow

**WAV / FLAC → Convert → OGG → Stream to Users**

## Organizing Data for Analysis

Data processing also makes information easier for analysts and data scientists to find and use.

Examples:

- Organizing data into tables.
- Extracting metadata from files.
- Storing metadata in databases.
- Converting raw data into a consistent structure.
- Fitting data into a predefined schema.

## Extracting Metadata

Music files may contain metadata such as:

- Artist name
- Genre

Data processing can extract this information and store it in a database.

This allows:

- Data analysts
- Data scientists
- Applications

to access the information more easily.

### Example

**Music File → Extract Metadata → Database**

## Fitting Data to a Schema

Data may need to conform to a specific structure.

For example, employee data can be organized into fields such as:

- Employee ID
- First Name
- Last Name
- Team
- Role
- Full-Time Status
- Office

Processing can also transform data into more appropriate representations.

For example:

- Separate first name and last name.
- Use a logical value to represent full-time or part-time status.

Instead of storing:

`Full-Time`

as text, the database could use:

`full_time = TRUE`

This makes the data more consistent and easier to analyze.

## Data Processing and Productivity

Data engineers automate as many repetitive data preparation tasks as possible.

The goal is to ensure that data reaches data scientists in a form that allows them to begin analysis almost immediately.

### Key Idea

**Automated Data Preparation → Faster Analysis → More Time for Insights**

Data scientists create value primarily through the **insights derived from their analyses**.

Data engineers support this by handling routine and repeatable preparation tasks.

# How Data Engineers Process Data

Data engineers have several responsibilities related to data processing.

## 1. Data Manipulation

Data engineers transform and manipulate data into the form needed by the organization.

## 2. Data Cleaning

Data engineers clean data and handle invalid or corrupted records.

Examples:

- Reject corrupted song files.
- Handle invalid records.
- Address missing information.

## 3. Data Tidying

Data engineers organize data into a logical and consistent structure.

The objective is to make data easier to:

- Understand
- Query
- Analyze
- Maintain

## 4. Handle Missing Data

Data engineers must determine what should happen when required information is missing.

For example, if a song's genre is missing, possible approaches include:

- Reject the file.
- Leave the genre blank.
- Assign a default value.

The correct approach depends on the organization's data quality requirements.

## 5. Maintain Well-Structured Databases

Data engineers ensure that data is stored in a sensible and organized database structure.

This includes:

- Properly organizing tables.
- Separating different entities.
- Maintaining relationships between tables.

## 6. Create Database Views

A **view** is the output of a **stored query** on database data.

Views can make data easier for analysts to access.

### Example

Artist data and album data may be stored in separate tables:

- `artists`
- `albums`

However, users may frequently need information from both tables together.

A data engineer can create a **view** that combines information from the two tables.

**Artists + Albums → View → Analyst**

The view allows analysts to access combined information more easily without repeatedly constructing the same query.

## 7. Optimize Database Performance

Data engineers optimize databases so data can be retrieved efficiently.

One example is **indexing**.

### Indexing

An **index** helps a database find and retrieve data more efficiently.

> **Indexing → Faster data retrieval**

# Data Processing Tools

There are many data processing tools available.

The course does not cover them in detail.

## Apache Spark

**Apache Spark** is one example of a data processing tool.

It is designed for large-scale data processing.

## Batch and Stream Processing

The course indicates that the difference between **batch processing** and **stream processing** will be discussed in the following lesson.

# Examples of Data Processing

### Audio

**WAV / FLAC → OGG**

Purpose:

- Reduce file size.
- Reduce network costs.
- Make streaming more efficient.

### Metadata

**Music File → Extract Artist / Genre → Database**

Purpose:

- Make metadata easier to access.
- Improve search and analysis.

### Employee Data

**Raw Employee Data → Clean / Transform → Structured Employee Table**

Purpose:

- Improve consistency.
- Follow a predefined schema.
- Make analysis easier.

### Database View

**Artists Table + Albums Table → View**

Purpose:

- Provide convenient access to related information.
- Simplify analyst queries.

### Data Validation

**Raw Track → Check Readability / Artist / Size / Format → Accept or Reject**

Purpose:

- Remove corrupted or invalid files.
- Maintain data quality.

# Data Processing vs. Data Storage

| Concept | Main Focus |
|---|---|
| **Data Storage** | Where and how data is stored |
| **Data Processing** | How data is transformed into useful information |
| **Data Engineering** | Building and managing systems that move, store, and process data |

# Exam / Interview Key Points

- **Data processing = converting raw data into meaningful information.**
- Data processing can involve:
  - Manipulation
  - Cleaning
  - Tidying
  - Transformation
  - Validation
  - Metadata extraction
  - Data organization
  - Compression
- Data processing can reduce **storage, processing, and network costs**.
- Uncompressed data can be **10× larger** than compressed data according to the lesson.
- Spotflix converts `.wav` and `.flac` master files into `.ogg` for streaming.
- `.ogg` is used because it is **lighter/smaller**, with slightly lower sound quality.
- Data processing can extract metadata such as **artist name and genre**.
- Data can be transformed to fit a specific **schema**.
- Data engineers automate repetitive preparation tasks so data scientists can analyze data sooner.
- Data engineers handle **data manipulation, cleaning, and tidying**.
- Data engineers decide how to handle **missing data**.
- Data engineers maintain well-structured databases.
- A **view** is the output of a stored query on database data.
- Views can combine information from multiple tables for easier access.
- **Indexing** improves data retrieval performance.
- **Apache Spark** is an example of a data processing tool.

# Quick Memory Aid

**Data Processing = Clean + Transform + Organize + Validate**

**Data Engineer = Prepare data so others can use it efficiently**

**View = Stored query output**

**Index = Faster retrieval**

**Spark = Data processing tool**

## Most Important Concept

> **Data processing converts raw data into meaningful, organized, and efficient-to-use information. Data engineers automate cleaning, transformation, validation, organization, and other recurring tasks so analysts and data scientists can focus on extracting insights.**
