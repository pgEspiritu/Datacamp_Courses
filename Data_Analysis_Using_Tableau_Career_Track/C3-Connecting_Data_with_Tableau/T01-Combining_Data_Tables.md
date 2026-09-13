# 📊 Combining Data Tables in Tableau

---

# 📖 Summary

Combining data is one of the first steps in data analysis because information is often spread across multiple files or tables. Tableau simplifies this process with a drag-and-drop interface, eliminating the need for manual coding. The two primary methods for combining data are **Unions** and **Joins**, each serving different purposes depending on how the data is organized.

---

# 📚 Key Concepts

## 1. Combining Data

Data rarely arrives in a single, analysis-ready table. It is commonly stored across multiple:

- CSV files
- Excel worksheets
- Database tables

Tableau allows users to combine these datasets quickly using visual tools.

---

## 2. Union

A **Union** combines tables by **adding rows** from one table beneath another (vertical stacking).

### When to Use a Union

Use a union when:

- The tables have the same structure.
- They contain the same columns.
- They represent different time periods (daily, monthly, quarterly, yearly).

### Requirements

For a successful union, tables should have:

- The same number of columns
- Similar column names
- Matching data types
- Preferably the same column order

### Example

A company stores sales data in separate files for each quarter. To analyze the entire year, all quarterly files are **unioned** into one larger dataset.

---

## 3. Join

A **Join** combines tables by **matching related records** using a common field (key or ID).

Unlike a union, joins add **columns**, not rows.

### When to Use a Join

Use a join when:

- Related information is stored in different tables.
- Tables share a common identifier.
- You want to enrich one table with information from another.

### Example

One table contains employee information, while another contains office locations.

Using **Location ID**, Tableau matches each employee with the correct office address.

---

## 4. Join Types

### Inner Join

Returns **only matching records** from both tables.

Use when you only need records that exist in both datasets.

---

### Left Join

Returns:

- All records from the **left table**
- Matching records from the **right table**

If no match exists, the right-side columns contain **Null** values.

This was the join used in the employee example because every employee was kept, including the remote employee who had no office location.

---

### Right Join

Returns:

- All records from the **right table**
- Matching records from the **left table**

Rows without matches on the left contain **Null** values.

---

### Full Outer Join

Returns:

- All matching records
- All unmatched records from both tables

Missing values are filled with **Null** where no match exists.

---

# 🚴 Example: Union

Quarterly Divvy Bike datasets can be unioned into a single table to analyze an entire year's worth of rides.

```
Q1
Q2
Q3
Q4
 │
 ▼
Full Year Dataset
```

---

# 🏢 Example: Join

Two related tables:

### Employees

| Employee | Location ID |
|-----------|-------------|
| Alice | 1 |
| John | 2 |
| Bob | Null |

### Offices

| Location ID | Address |
|-------------|---------|
| 1 | New York |
| 2 | Chicago |
| 3 | London |

Using a **Left Join** produces:

| Employee | Location ID | Address |
|-----------|-------------|---------|
| Alice | 1 | New York |
| John | 2 | Chicago |
| Bob | Null | Null |

Bob remains in the result because the left join keeps every employee, even when no matching office exists.

---

# 🛒 Superstore Dataset

The lesson introduces Tableau's **Superstore** dataset, which contains **seven tables**:

### Orders (2016–2020)

Five annual tables containing:

- Order ID
- Products
- Customers
- Sales Representatives
- Order Dates
- Locations
- Sales information

### Returns

Contains the Order IDs of returned products.

### Sales Reps

Maps sales representatives to their assigned regions.

These tables will later be combined using **Unions** and **Joins** to create a complete dataset for analysis.

---

# 🎯 Key Takeaways

- Data is often stored across multiple files or tables.
- Tableau provides a drag-and-drop interface for combining datasets.
- **Union** stacks tables vertically by adding rows.
- **Join** combines tables horizontally by matching related records.
- Joins rely on a shared key or identifier.
- The four join types are **Inner**, **Left**, **Right**, and **Full Outer**.
- Use **Unions** for datasets with identical structures.
- Use **Joins** for related datasets that share common keys.
- The Superstore dataset demonstrates both techniques using annual orders, returns, and sales representative data.
