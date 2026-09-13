# 💾 Tableau Extracts and File Types

---

# 📖 Summary

Tableau provides several file types for saving, sharing, and working with data. Understanding these file types helps you choose the best option based on your workflow, whether you're collaborating with others, working offline, or analyzing large datasets.

One of the most important file types is the **Extract**, which creates a local copy of your data. Extracts improve performance, support very large datasets, preserve data preparation work, and allow offline analysis. Tableau also offers **Live Connections**, which connect directly to the original data source and always display the most current data.

---

# 📚 Key Concepts

## 1. Tableau File Types

Tableau supports several file types for different purposes.

### Packaged Workbook (.twbx)

A **Packaged Workbook** contains:

- The workbook
- Local datasets
- Images
- Other supporting files

Everything is bundled into a single compressed file, making it ideal for sharing with users who do not have access to the original data.

**Best for:**

- Sharing complete Tableau projects
- Portability
- Sending work to others

---

### Workbook (.twb)

A **Workbook** contains only the Tableau workbook itself.

The actual data files are **linked**, not included.

**Advantages**

- Smaller file size
- Easy to manage when everyone has access to the same data source

**Limitation**

- Cannot be opened correctly if the linked data files are unavailable.

---

### Extract (.hyper / .tde)

An **Extract** is a local snapshot of part or all of a data source.

Modern versions of Tableau use the **.hyper** format, while older versions used **.tde**. Existing `.tde` files are automatically upgraded to `.hyper` in newer Tableau versions.

Extracts are optimized for speed using Tableau's **Hyper** database engine.

---

### Data Source Files

A **Data Source File** stores:

- Connection information
- Data source settings
- Calculated fields
- Groups
- Other data preparation configurations

These files simplify reconnecting to prepared data sources.

---

## 2. What is a Tableau Extract?

A Tableau **Extract** is a local copy of your data that has been optimized for analysis.

Instead of querying the original data source every time, Tableau reads data directly from the extract.

This significantly improves performance while preserving your data preparation work.

---

## 3. Benefits of Extracts

Extracts offer several important advantages:

- Faster workbook loading and saving
- Faster filtering and interaction
- Optimized using the Hyper database engine
- Support for billions of rows of data
- Preserve joins, unions, and relationships
- Retain calculated fields and data transformations
- Enable offline analysis
- Reduce dependence on network connectivity

Because extracts store prepared data locally, they are generally much faster than repeatedly querying external databases.

---

## 4. Live Connections

A **Live Connection** keeps Tableau directly connected to the original data source.

The source may be:

- Excel files
- SQL databases
- Cloud databases
- Enterprise data warehouses
- Amazon Redshift and other database systems

Whenever the underlying data changes, Tableau displays the updated information automatically.

---

## 5. Extract vs. Live Connection

| Extract | Live Connection |
|----------|-----------------|
| Local copy of the data | Direct connection to the original source |
| Faster performance | Slower performance (depends on the source) |
| Uses Hyper engine | Queries the source database each time |
| Supports offline work | Requires access to the data source |
| Requires manual or scheduled refresh | Updates automatically with source changes |
| Best for large datasets and analysis | Best for real-time reporting |

---

## 6. When to Use Each

### Use an Extract when:

- Performance is important.
- Working with very large datasets.
- Working offline.
- Sharing prepared data.
- Reducing database queries.
- Preserving data preparation work.

### Use a Live Connection when:

- Real-time data is required.
- The data changes frequently.
- Users always need the latest information.
- Network connectivity is reliable.
- Data must remain in the original source.

---

# 🎯 Key Takeaways

- Tableau offers multiple file types for saving and sharing work.
- **.twbx** packages the workbook and supporting files into one portable file.
- **.twb** contains only the workbook and references external data sources.
- **.hyper** extracts store optimized local copies of data.
- Extracts improve performance and support offline analysis.
- The **Hyper** engine enables fast processing of very large datasets.
- Live Connections always retrieve the latest data directly from the source.
- Extracts require refreshing to reflect changes in the original data.
- Choose **Extracts** for speed and offline work, and **Live Connections** for real-time reporting.
