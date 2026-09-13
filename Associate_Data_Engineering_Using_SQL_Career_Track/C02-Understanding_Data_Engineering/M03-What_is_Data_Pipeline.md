# Data Pipelines

## What Is a Data Pipeline?

A **data pipeline** is a system or process that moves data efficiently from one system or stage to another.

Data pipelines automate the flow of data so that data scientists and other users can access **up-to-date, accurate, and relevant data**.

### Main Purposes

Data pipelines help to:

- Automate data movement.
- Reduce human intervention.
- Reduce errors.
- Decrease the time required for data to flow through an organization.
- Ensure data reaches the appropriate destination in the appropriate form.

## "Data Is the New Oil" Analogy

Data pipelines can be compared to oil pipelines and oil-processing systems.

The oil process involves:

**Extraction → Transportation → Processing → Storage/Distribution → Final Users**

Similarly, data goes through:

**Data Sources → Ingestion → Processing/Transformation → Storage → Analysis/Applications**

The analogy shows that raw data, like crude oil, needs to be **moved, processed, transformed, stored, and delivered** before it can provide value.

## Spotflix Data Pipeline

Spotflix receives data from multiple sources, including:

- Mobile application
- Desktop application
- Spotflix website
- Internal websites and systems
- HR management system

A simplified Spotflix workflow is:

**Mobile App / Desktop App / Website / Internal Systems → Data Ingestion → Data Lake → Databases → Data Scientists / Applications**

## Data Lake

The data from different sources is ingested into a **data lake**.

> A data lake is a storage system used to store large amounts of data, often in its raw or original form.

The course discusses data lakes in more detail in the next chapter.

## Examples of Spotflix Databases

### Artists Database

May contain:

- Artist name
- Number of followers
- Associated acts

### Albums Database

May contain:

- Label
- Producer
- Year of release

### Tracks Database

May contain:

- Track name
- Track length
- Featured artists
- Number of listens

### Playlists Database

May contain:

- Playlist name
- Songs contained
- Date of creation

### Customers Database

May contain:

- Username
- Account opening date
- Subscription tier

### Employees Database

May contain:

- Employee name
- Salary
- Reporting manager

## Data Organization

Data pipelines can organize data into different tables or databases.

For example, employee data can be separated by:

**Employees → Department → Office**

Departments:

- Sales
- Engineering
- Support

Offices:

- USA
- Belgium
- UK

This organization allows data scientists to analyze specific datasets, such as investigating **employee turnover**.

## Data Validation and Processing

Data pipelines can also validate and process data before it is stored in a clean database.

For tracks, the pipeline may:

- Check whether the track is readable.
- Check whether the corresponding artist exists in the database.
- Check whether the file has the correct size.
- Check whether the file has the correct format.
- Identify and handle corrupted or invalid data.

After processing:

**Raw Tracks → Validation / Processing → Clean Tracks Database → Data Scientists**

The clean tracks database can be used to analyze song similarity and build a **recommendation engine**.

## What Data Pipelines Automate

Data pipelines can automate:

- **Extracting** data
- **Transforming** data
- **Combining** data
- **Validating** data
- **Loading** data

### Benefits

- Less human intervention
- Fewer errors
- Faster data movement
- More efficient workflows
- More reliable data
- More up-to-date data

# ETL

**ETL** stands for:

- **E = Extract**
- **T = Transform**
- **L = Load**

ETL is a popular framework for designing data pipelines.

### ETL Process

**Extract → Transform → Load**

### Extract

Retrieve data from a source system.

### Transform

Process or modify the data before storing it.

Examples:

- Clean data
- Validate data
- Change formats
- Combine data
- Organize data

### Load

Store the transformed data in a destination system, such as a database.

## Key ETL Concept

> In ETL, **data is transformed before it is stored** in the destination.

## Data Pipeline vs. ETL

**Data pipeline** and **ETL** are related but are not the same thing.

### Data Pipeline

A **data pipeline** is a broader process for moving data from one system or stage to another.

A pipeline may:

- Extract data.
- Transform data.
- Validate data.
- Combine data.
- Load data.
- Route data to applications.
- Move data without transforming it.

### ETL

**ETL is a specific approach to building a data pipeline:**

**Extract → Transform → Load**

The defining characteristic is that the data is **transformed before it is loaded into the destination**.

## Key Difference

| Concept | Data Pipeline | ETL |
|---|---|---|
| **Definition** | Process/system for moving data | Specific data integration approach |
| **Scope** | Broader | More specific |
| **Transformation** | May or may not occur | Occurs before loading |
| **Main idea** | Move data efficiently | Extract → Transform → Load |
| **Destination** | Database, application, visualization tool, etc. | Usually a destination database/storage system |

> **Not all data pipelines are ETL pipelines.**

For example, a pipeline can move data directly to a visualization tool or Salesforce without transforming it first.

## Exam / Interview Key Points

- A **data pipeline** efficiently moves data from one system or stage to another.
- Data pipelines automate the flow of data.
- Data pipelines reduce **human intervention and errors**.
- Data pipelines decrease the **time required for data to flow through an organization**.
- Data pipelines can **extract, transform, combine, validate, and load** data.
- **ETL = Extract, Transform, Load**.
- In ETL, data is **transformed before it is loaded/stored**.
- **Not all data pipelines use ETL**.
- A pipeline may move data without transformation.
- A pipeline may route data directly to applications or visualization tools.
- Data pipelines provide data scientists with **up-to-date, accurate, and relevant data**.
- Data engineers are responsible for designing and maintaining data pipelines.
- Data pipelines can be used to validate data, such as checking file readability, size, format, and related database records.

## Quick Memory Aid

**Data Pipeline = Move data**

**ETL = Extract → Transform → Load**

**Pipeline = Broader concept**

**ETL = One specific approach to building a pipeline**

## Most Important Concept

> **Data pipelines automate the efficient flow of data through an organization, while ETL is a specific approach where data is extracted, transformed, and then loaded into a destination system.**
