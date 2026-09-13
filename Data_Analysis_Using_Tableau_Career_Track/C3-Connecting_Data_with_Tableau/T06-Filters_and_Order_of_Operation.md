# 🔍 Filters and Tableau's Order of Operations

---

# 📖 Summary

Filters allow you to limit the data displayed and analyzed in Tableau. Because multiple filters can be applied simultaneously, Tableau follows a specific **Order of Operations** to determine the sequence in which filters are processed. Understanding this order is essential because earlier filters affect the data available to later filters, influencing both performance and analysis results.

---

# 📚 Key Concepts

## 1. Tableau's Order of Operations

When multiple filters are applied, Tableau processes them in the following order:

1. **Extract Filters**
2. **Data Source Filters**
3. **Context Filters**
4. **Dimension Filters**
5. **Measure Filters**
6. **Table Calculation Filters**

Each filter operates on the output of the previous filter, making the order important for both accuracy and performance.

---

## 2. Extract Filters

Extract Filters limit the data that is copied into a **Tableau Extract (.hyper)**.

### Characteristics

- Only available when using **Extract Connections**
- Applied before the data is imported into Tableau
- Reduce the size of the extract
- Improve workbook performance

### Common Uses

- Import only recent records
- Exclude unnecessary data
- Reduce storage requirements

---

## 3. Data Source Filters

Data Source Filters restrict data at the data source level.

### Characteristics

- Work with both **Live Connections** and **Extracts**
- Apply to every worksheet using the data source
- Prevent unwanted records from being loaded into visualizations

### Common Uses

- Restrict data for different user groups
- Exclude confidential records
- Create organization-wide filtering rules

---

## 4. Context Filters

A **Context Filter** creates a temporary subset of data that Tableau uses before applying other worksheet filters.

Instead of repeatedly filtering the entire dataset, Tableau filters the smaller context dataset first.

### Benefits

- Improves query performance
- Makes dependent filters faster
- Limits the data processed by subsequent filters

---

### Example

Suppose your dataset contains sales from many countries and product categories.

Without a Context Filter:

- Filter **Category = Furniture**
- Filter **Country = Germany**

Each filter searches the **entire dataset** independently.

With a Context Filter:

```
Entire Dataset
        │
        ▼
Context Filter
(Category = Furniture)
        │
        ▼
Dimension Filter
(Country = Germany)
```

Now the Country filter searches only the Furniture records, reducing the amount of data Tableau processes.

---

## 5. Dimension Filters

Dimension Filters use **categorical fields** to filter data.

Examples include:

- Country
- Region
- Product Category
- Customer Name
- Department

These filters determine which categories or groups appear in the visualization.

---

## 6. Measure Filters

Measure Filters use **numeric values** to limit data.

Examples include:

- Sales
- Profit
- Quantity
- Discount
- Revenue

These filters commonly use conditions such as:

- Greater than
- Less than
- Between
- Top N values

---

## 7. Table Calculation Filters

Table Calculation Filters are applied **last**, after all other filters and calculations have been processed.

They filter the results of table calculations rather than the underlying data.

Examples include filtering based on:

- Running totals
- Rankings
- Percent of total
- Moving averages

---

# 📊 Tableau Filter Order

```
Data Source
      │
      ▼
Extract Filter
      │
      ▼
Data Source Filter
      │
      ▼
Context Filter
      │
      ▼
Dimension Filter
      │
      ▼
Measure Filter
      │
      ▼
Table Calculation Filter
      │
      ▼
Visualization
```

---

# 🎯 When to Use Each Filter

| Filter Type | Purpose |
|-------------|---------|
| Extract Filter | Reduce the data included in an extract |
| Data Source Filter | Restrict records available from the data source |
| Context Filter | Create a subset of data for faster filtering |
| Dimension Filter | Filter categorical fields |
| Measure Filter | Filter numeric values |
| Table Calculation Filter | Filter calculated results after aggregation |

---

# 🎯 Key Takeaways

- Tableau applies filters in a predefined **Order of Operations**.
- **Extract Filters** are applied first and only work with data extracts.
- **Data Source Filters** limit the records available from the data source for all worksheets.
- **Context Filters** create a temporary subset of data that improves performance and influences later filters.
- **Dimension Filters** filter categorical data such as names, regions, and categories.
- **Measure Filters** filter numeric values such as sales and profit.
- **Table Calculation Filters** are processed last and operate on calculated results rather than the raw data.
- Understanding the filter order helps improve dashboard performance and ensures accurate analytical results.
