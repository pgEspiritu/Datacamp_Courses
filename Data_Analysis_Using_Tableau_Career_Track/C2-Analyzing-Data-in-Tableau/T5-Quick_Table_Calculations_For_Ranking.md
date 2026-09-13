# ⚡ Quick Table Calculations for Ranking (Tableau Lesson) — Summary

---

## 🎯 Key Takeaway

Quick Table Calculations in Tableau are powerful tools that allow analysts to perform calculations directly on values shown in a visualization. They help users quickly generate insights such as rankings, percentages, running totals, and differences without manually building complex formulas.

---

## 📊 What Is a Table Calculation?

A **table calculation** is a computation performed on data that is already visible in a visualization.

### Key Difference

- **Standard Calculations** → operate on raw underlying data  
- **Table Calculations** → operate on displayed (filtered and visualized) data

### Examples of Table Calculations

- Running Total  
- Rank  
- Percent of Total  
- Difference  
- Moving Average  
- Percent Difference  

---

## ⚠️ Important Behavior

Table calculations only consider:

- Data currently shown in the view

They do NOT include:

- Filtered-out dimensions
- Filtered-out measures
- Hidden data not present in the visualization

This makes them **view-dependent calculations**.

---

## 🧩 Two Core Concepts

Table calculations are defined by:

### 1. Scope

The **scope** defines *which group of data* the calculation applies to.

#### Example

If scope = Continent:

- Each continent is calculated independently
- Results do not mix across continents

| Continent | Calculation Behavior |
|------------|----------------------|
| Asia | Independent calculation |
| Europe | Independent calculation |
| North America | Independent calculation |

---

### 2. Direction

The **direction** defines *how the calculation moves through the data*.

### Common Directions

- Across
- Down
- Across then Down
- Down then Across

### Example

If direction = Across:

- Values are processed horizontally
- Calculation moves left → right across time or categories

---

## ➕ Example: Running Total

A **running total** continuously adds values over time.

### How It Works

For each row:

1. Take previous total
2. Add current value
3. Output cumulative result

### Example Table

| Year | Value | Running Total |
|------|-------|---------------|
| Year 1 | 100 | 100 |
| Year 2 | 150 | 250 |
| Year 3 | 200 | 450 |
| Year 4 | 120 | 570 |

---

## ⚡ What Are Quick Table Calculations?

**Quick Table Calculations** are pre-built table calculations in Tableau that can be applied instantly without manual setup.

### Key Features

- Preconfigured calculation types
- Automatically applied scope and direction
- Fast setup and execution
- Designed for common analytical needs

### Tableau Intelligence

Tableau automatically:

- Enables only valid calculations for the current view
- Disables irrelevant options

This prevents incorrect configurations.

---

## 🏆 Practical Use Cases in This Course

Quick Table Calculations are used to analyze:

### 🚲 Station Performance

- Rank most popular stations
- Identify least used stations
- Compare activity levels

### 👥 Customer Demographics

- Percentage of male vs female riders
- Age group distribution
- User segmentation

### 🚴 Rider Types

- Subscriber vs customer proportions
- Usage distribution across groups

---

## 📊 Why Quick Table Calculations Matter

They help analysts:

- Save time on calculations
- Avoid complex formulas
- Explore data interactively
- Build insights faster
- Enhance dashboards with dynamic metrics

---

## 🧠 Key Concepts Summary

### Table Calculation = View-Based Computation

Operates only on visible data in a visualization.

---

### Scope

Defines:

- *Where* the calculation applies
- Example: per continent, per category, per station

---

### Direction

Defines:

- *How* the calculation flows through data
- Example: across rows, down columns

---

### Running Total

A cumulative sum that builds over time:

- Adds each value to the previous total

---

## 🚀 Summary

Quick Table Calculations in Tableau provide an efficient way to compute rankings, percentages, and cumulative metrics directly within visualizations. By understanding **scope** and **direction**, analysts can correctly interpret results and create powerful insights. These tools are essential for ranking stations, analyzing customer demographics, and exploring Divvy bike usage patterns effectively.
