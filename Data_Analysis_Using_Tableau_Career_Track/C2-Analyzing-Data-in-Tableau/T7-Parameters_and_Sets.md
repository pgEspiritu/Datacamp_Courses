# 🎛️ Parameters and Sets (Tableau Lesson) — Summary

---

## 🎯 Key Takeaway

**Parameters** and **Sets** are powerful Tableau features that add interactivity and flexibility to data analysis.

- **Parameters** let users control values dynamically.
- **Sets** divide data into two groups: **IN** and **OUT**.

Together, they help create interactive dashboards and deeper analytical insights.

---

# 🎛️ Parameters

## 📌 What Are Parameters?

A **Parameter** is a global, user-controlled value (number, date, or string) that can replace a constant in:

- Calculations  
- Filters  
- Reference lines  

👉 Think of parameters as **inputs that users can change dynamically**.

---

## ⚡ Why Use Parameters?

Parameters allow users to:

- Change values interactively
- Explore different scenarios
- Customize dashboards
- Control calculations and filters
- Analyze “what-if” situations

---

## 🎚️ How Parameters Work

Parameters work through a **Parameter Control**, which allows users to:

- Enter values manually
- Select from a list
- Use sliders

This updates the visualization instantly.

---

## 📊 Example: Top N Stations

Instead of a fixed view:

- Top 15 stations

A parameter allows users to change it to:

- Top 10
- Top 25
- Top 50
- Top 100

👉 No need to edit the worksheet.

---

## 🧠 Common Parameter Use Cases

### 💰 Budget Scenarios
- Adjust budget values (e.g., $25K → $100K)
- See how results change dynamically

### 📅 Date Filtering
- Select specific start/end dates
- Focus on custom time periods

### 🏆 Ranking Control
- Adjust Top N customers or stations
- Dynamically change leaderboard size

---

## 🔗 Parameters in Tableau

Parameters can be used with:

- 🧮 Calculated Fields
- 🔍 Filters
- 📏 Reference Lines

They appear in the **Data Pane** under their own section.

---

# 🧩 Sets

## 📌 What Are Sets?

A **Set** is a custom subset of data that divides values into:

- **IN** → selected members  
- **OUT** → all other members  

👉 Everything is classified as either IN or OUT.

---

## ⚡ Why Use Sets?

Sets are useful for:

- Segmentation
- Comparison
- Highlighting selected data
- Creating reusable subsets

---

## 🔄 How Sets Work

### Example

| Product |
|----------|
| A |
| B |
| C |
| D |

If we select A and B:

| Product | Status |
|----------|--------|
| A | IN |
| B | IN |
| C | OUT |
| D | OUT |

---

## 📊 Example Use Cases for Sets

### 🏆 High Sales Products

- IN → Products above sales threshold
- OUT → Products below threshold

### 🎉 Public Holidays

- IN → Holiday dates
- OUT → Non-holiday dates

### 👥 Selected Customers

- IN → Target customers
- OUT → Others

---

## ⚠️ Limitation of Sets

Sets only support **two categories**:

- IN
- OUT

If more categories are needed, use:

- 🗂️ Groups
- 🧮 Calculated Fields

---

# ⚖️ Parameters vs Sets

| Feature | Purpose | Categories |
|----------|--------|-------------|
| Parameter | User input control | Variable |
| Set | Data segmentation | IN / OUT |
| Group | Categorization | Multiple |
| Calculated Field | Logic-based classification | Multiple |

---

# 🧠 When to Use Each Tool

## 🎛️ Use Parameters When:
- Users need control over values
- Dashboards require interactivity
- You need “what-if” analysis
- Values must change dynamically

---

## 🧩 Use Sets When:
- You need IN vs OUT segmentation
- You want to highlight selected data
- You are building reusable subsets
- You need simple comparisons

---

## 🗂️ Use Groups When:
- You need multiple categories
- You want to consolidate similar values
- You need cleaner classifications

---

## 🧮 Use Calculated Fields When:
- Logic is complex
- Multiple conditions are needed
- Custom formulas are required

---

# 📊 Tableau Tools Overview

| Tool | Purpose |
|------|--------|
| Filters | Restrict data shown |
| Calculated Fields | Create new logic-based values |
| Groups | Combine related values |
| Sets | Create IN/OUT subsets |
| Parameters | User-controlled inputs |
| Quick Table Calculations | Fast analytics on visual data |

---

# 🚀 Summary

Parameters and Sets extend Tableau’s analytical power:

- **Parameters** make dashboards interactive and flexible.
- **Sets** allow quick segmentation into IN and OUT groups.

Together, they enable more dynamic, customizable, and insightful visualizations that go beyond static analysis.
