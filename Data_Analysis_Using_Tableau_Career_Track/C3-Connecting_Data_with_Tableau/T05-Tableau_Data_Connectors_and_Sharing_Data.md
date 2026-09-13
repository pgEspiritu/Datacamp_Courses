# 🔌 Tableau Data Connectors and Sharing Data

---

# 📖 Summary

Tableau can connect to a wide variety of data sources, making it easy to analyze information from files, databases, cloud platforms, and Tableau servers. It provides native connectors for over 80 different data environments and supports additional connection methods through JDBC, ODBC, and Web Data Connectors.

After preparing a data source, Tableau allows you to save the connection as a **Data Source (.tds)** file. This file stores connection information and customizations—not the actual data—making it easy to reuse and share data connections with others who have access to the original data.

---

# 📚 Key Concepts

## 1. Tableau Data Connectors

Tableau Desktop supports connecting to many different types of data sources through the **Connect** page.

There are four primary connection categories:

### Tableau Server

Connect to:

- Tableau Server
- Tableau Cloud
- Tableau Public

This allows you to access published datasets and shared organizational data.

---

### Files

Connect directly to local files such as:

- Microsoft Excel
- CSV (Text Files)
- PDF
- JSON
- Microsoft Access
- Statistical files (SPSS, SAS, etc.)

This option is commonly used for standalone datasets.

---

### Servers

Connect to database servers and cloud data platforms, including:

- Microsoft SQL Server
- MySQL
- PostgreSQL
- Oracle
- Snowflake
- Teradata
- Google BigQuery
- Amazon Redshift
- Google Analytics
- Google Sheets

These connections enable analysis of enterprise-scale data.

---

### Saved Data Sources

After connecting to and customizing a data source, Tableau allows you to save it as a reusable connection.

Saved Data Sources appear on the **Connect** page, making it faster to reconnect to frequently used datasets.

---

## 2. Native Connectors

Tableau provides **native connectors** for more than **80** popular data platforms.

Benefits include:

- Easy setup
- Optimized performance
- Secure authentication
- Seamless integration

These connectors reduce the need for manual configuration.

---

## 3. Other Connection Options

If your data source is not listed, Tableau offers additional connection methods.

### JDBC (Java Database Connectivity)

Allows Tableau to connect to many databases using JDBC drivers.

---

### ODBC (Open Database Connectivity)

Provides a standardized method for connecting to databases through ODBC drivers.

---

### Web Data Connector (WDC)

Enables Tableau to connect to web-based APIs and online services that do not have built-in connectors.

These options expand Tableau's compatibility with a wide range of data sources.

---

## 4. Tableau Desktop vs. Tableau Public

The available connectors differ depending on the Tableau edition.

| Tableau Desktop | Tableau Public |
|-----------------|----------------|
| Access to all supported connectors | Limited file connectors |
| Extensive database support | Only a few server connections |
| Can save Data Source (.tds) files | Cannot save .tds files |
| Designed for professional and enterprise use | Designed for public sharing and learning |

Tableau Desktop offers significantly more connectivity and data management features than Tableau Public.

---

## 5. Sharing Data with Data Source Files (.tds)

A **Tableau Data Source (.tds)** file stores the information needed to reconnect to a data source.

It contains:

- Connection information
- Calculated fields
- Groups
- Default properties
- Filters
- Other data source customizations

A `.tds` file **does not** contain the actual data.

Instead, it acts as a shortcut to the original data source.

---

## 6. When to Use a TDS File

Use a **.tds** file when:

- Multiple users need the same customized data source.
- Everyone has access to the original database or file.
- You want to reuse calculated fields and data preparation work.
- You want consistent data connections across projects.

Because the data itself is not stored inside the `.tds` file, recipients must be able to access the original data source.

---

# 📊 Common Tableau Connection Types

| Connection Type | Purpose |
|-----------------|---------|
| Tableau Server | Connect to published Tableau data |
| Files | Connect to local files such as Excel and CSV |
| Servers | Connect to databases and cloud platforms |
| Saved Data Sources | Reuse customized data connections |
| JDBC | Connect to databases using Java drivers |
| ODBC | Connect to databases using standard drivers |
| Web Data Connector | Connect to web APIs and online services |

---

# 🎯 Key Takeaways

- Tableau can connect to files, databases, cloud services, and Tableau servers.
- Tableau Desktop supports over **80 native data connectors**.
- Additional databases can be accessed using **JDBC**, **ODBC**, or the **Web Data Connector**.
- **Tableau Desktop** offers significantly more connection options than **Tableau Public**.
- A **.tds** file stores connection settings and customizations but **does not contain the actual data**.
- Data Source files are ideal for reusing and sharing customized data connections among users with access to the original data source.
