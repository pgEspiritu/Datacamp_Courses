# 🔗 Relationships in Tableau

---

# 📖 Summary

**Relationships** are a modern way to combine data in Tableau. Introduced in **May 2020**, they allow tables to remain separate while defining how they are related through common fields. Unlike joins, relationships do not immediately merge tables. Instead, Tableau determines the most appropriate way to combine the data based on the visualization being created.

Relationships provide greater flexibility, preserve the original level of detail in each table, and reduce the need for extensive data preparation before analysis.

---

# 📚 Key Concepts

## 1. What Are Relationships?

A **Relationship** defines how two or more tables are connected using one or more common fields.

Unlike joins:

- Tables remain separate.
- No new combined table is created.
- Each table keeps its own level of detail.
- Tableau combines data only when needed during analysis.

---

## 2. How Relationships Work

A relationship is created by selecting one or more matching fields between tables.

For example:

```
Orders 2016–2020
        │
 Product Name
        │
Manufacturers.csv
```

Here, **Product Name** acts as the relationship field connecting the two logical tables.

Tableau treats this relationship as a **contract** between the tables, using it to determine how data should be combined whenever fields from both tables are used in a visualization.

---

## 3. Logical Tables

When using relationships:

- Each table remains an independent **logical table**.
- Tableau does not physically merge the tables.
- Relationships exist only as metadata describing how the tables are connected.

This preserves the original structure and granularity of each dataset.

---

## 4. Relationships vs. Joins

| Relationships | Joins |
|--------------|-------|
| Tables remain separate | Tables are physically combined |
| Join type is determined automatically | Join type must be chosen manually |
| Dynamic and context-aware | Static and fixed |
| Preserves each table's level of detail | Can duplicate or remove records |
| Requires less upfront data preparation | Often requires careful planning |

---

## 5. Dynamic Join Behavior

One of the biggest advantages of relationships is that Tableau automatically determines the most appropriate join type based on the visualization.

Instead of deciding between:

- Inner Join
- Left Join
- Right Join
- Full Outer Join

Tableau evaluates the fields used in the worksheet and generates the appropriate query behind the scenes.

This allows analysts to focus on building visualizations rather than managing join logic.

---

## 6. Benefits of Relationships

Relationships provide several advantages:

- Reduce the need for complex data preparation.
- Eliminate the need to choose a join type upfront.
- Preserve detailed records from multiple tables.
- Minimize the risk of losing unmatched records.
- Simplify analysis by allowing Tableau to handle data combinations automatically.
- Adapt dynamically to different visualizations.

These benefits make relationships especially valuable in enterprise environments where datasets are large and complex.

---

# 🆚 Relationships vs. Joins

### Relationships

```
Orders
    │
(Product Name)
    │
Manufacturers
```

- Tables stay separate.
- Tableau decides how to combine them when needed.
- More flexible and dynamic.

---

### Joins

```
Orders
      +
Manufacturers
      │
      ▼
Combined Table
```

- Tables are merged immediately.
- Join type is fixed before analysis.
- Changing the join later can affect existing worksheets.

---

# 🎯 Key Takeaways

- **Relationships** were introduced in Tableau in **May 2020**.
- A relationship defines how tables are connected without physically merging them.
- Tables remain as separate logical tables.
- Relationships are based on one or more common fields.
- Tableau automatically determines the appropriate join behavior during analysis.
- Relationships preserve each table's level of detail.
- They reduce the need for extensive data preparation and manual join management.
- Compared to joins, relationships are more flexible, dynamic, and easier to maintain for complex datasets.
