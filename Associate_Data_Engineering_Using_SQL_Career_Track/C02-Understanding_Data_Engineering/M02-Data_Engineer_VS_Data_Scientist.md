# Data Engineers vs. Data Scientists

## Data Workflow

Data engineers and data scientists work at different stages of the data workflow.

## Data Engineers

Data engineers focus on the **first part of the workflow**:

- Ingest data.
- Store data.
- Make data easily accessible.
- Make data ready for analysis.
- Build data pipelines.
- Optimize databases for analysis.

> **Data Engineer = Builds and maintains the data foundation.**

## Data Scientists

Data scientists focus on the **rest of the workflow**:

- Prepare data according to analysis needs.
- Explore data.
- Build visualizations.
- Run experiments.
- Build predictive models.
- Generate insights from data.

> **Data Scientist = Uses data to perform analysis, experiments, and predictive modeling.**

## How Data Engineers Enable Data Scientists

### Spotflix Example

- **Vivian** = Data Engineer
- **Julian** = Data Scientist

### Data Engineer: Vivian

Vivian:

- Collects and stores customer data.
- Collects and stores artist data.
- Collects and stores song data.
- Maintains the respective databases.
- Optimizes databases for analysis.
- Ensures information is easy to retrieve.
- Builds data pipelines.
- Makes tracks, artists, and listening-session data easily accessible.
- Keeps listening-session data up to date through pipelines.

### Data Scientist: Julian

Julian:

- Uses the databases provided by Vivian.
- Analyzes listening patterns.
- Builds recommendation engines.
- Uses tracks, artists, and listening-session data.
- Uses the outputs of data pipelines.
- Performs analysis without needing excessive data preparation.

## Data Engineer vs. Data Scientist

| Aspect | Data Engineer | Data Scientist |
|---|---|---|
| **Main focus** | Data infrastructure | Data analysis |
| **Workflow** | Ingest and store data | Prepare, explore, analyze, experiment, predict |
| **Data pipelines** | Builds pipelines | Uses pipeline outputs |
| **Databases** | Creates, updates, transforms, and optimizes | Queries and analyzes |
| **Primary expertise** | Software | Analytics |
| **Typical languages** | Python, Java, SQL | Python, R, SQL |
| **Goal** | Make reliable and accessible data available | Extract insights and build predictive models |

## Programming Languages

### Data Engineers

Generally more **software-oriented**.

Common languages:

- **Python**
- **Java**
- **SQL**

Uses include:

- Creating databases
- Updating databases
- Transforming databases
- Building data pipelines

### Data Scientists

Generally more **analytics-oriented**.

Common languages:

- **Python**
- **R**
- **SQL**

Uses include:

- Querying databases
- Analyzing data
- Exploring datasets
- Building visualizations
- Running experiments
- Building predictive models

## SQL

Both data engineers and data scientists use **SQL**, but for different purposes.

- **Data Engineers:** Use SQL to create, update, and transform databases.
- **Data Scientists:** Use SQL to query databases, meaning to request and retrieve information.

## Key Relationship

**Data Engineer → Builds the foundation → Data Scientist → Uses the data**

```text
Data Engineer
     ↓
Ingest & Store Data
     ↓
Optimize Databases
     ↓
Build Data Pipelines
     ↓
Provide Accessible Data
     ↓
Data Scientist
     ↓
Prepare & Explore Data
     ↓
Visualize & Analyze
     ↓
Experiments / Predictive Models
```

## Exam / Interview Key Points
- Data engineers focus primarily on ingesting and storing data.
- Data scientists focus on preparing, exploring, visualizing, analyzing, experimenting, and building predictive models.
- Data engineers build data pipelines.
- Data scientists use the outputs of data pipelines.
- Data engineers optimize databases so information is easy to retrieve and analyze.
- Data engineers are generally software experts.
- Data scientists are generally analytics experts.
- Data engineers commonly use Python, Java, and SQL.
- Data scientists commonly use Python, R, and SQL.
- Both roles use SQL, but data engineers use it for database creation/update/transformation while data scientists primarily use it for querying.
- Data engineers enable data scientists by providing accessible, well-structured, and analysis-ready data.

---

## Quick Memory Aid

**Data Engineer** = Build the data foundation

**Data Scientist** = Analyze and exploit the data

Engineer builds → Scientist uses

Engineer = Software → Scientist = Analytics
