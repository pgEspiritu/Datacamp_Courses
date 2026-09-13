# 📊 Dashboards and Stories in Tableau

---

## 1. Introduction 🚀

In the final part of this course, you'll learn about two powerful Tableau features:

- 📋 Dashboards
- 📖 Stories

As you create more visualizations, it becomes useful to display them together in a single view. Tableau dashboards make this possible.

---

## 2. What is a Dashboard? 📋

A **Dashboard** is a collection of multiple visualizations displayed on a single page.

### 🎯 Purpose:
- Compare data from different perspectives
- Monitor key metrics
- Discover insights more efficiently
- Create interactive reports

### Example:
A dashboard built using a video game dataset may contain:
- 🎮 Sales by platform
- 🏆 Top-selling video games
- 📈 Sales trends
- 🎯 Top game genres

All displayed in one location.

---

## 3. Dashboard Features ⚙️

### 🔗 Automatically Connected to Worksheets

Dashboards are linked directly to their underlying worksheets.

This means:

✅ Changes made to a worksheet automatically appear in the dashboard.

✅ Changes reflected in the dashboard remain connected to the source worksheet.

---

### 🖱️ Interactive Analysis

Dashboards can include:

- 🎛️ Filters
- 🔍 Drill-down functionality
- 📊 Interactive exploration

Users can investigate data without modifying the underlying worksheet.

---

### 🔄 Connected Views

One visualization can act as a filter for another.

### Example:
Clicking a region on a map could automatically update:
- Sales charts
- Product rankings
- KPI indicators

This creates a highly interactive user experience.

---

## 4. What is a Story? 📖

A **Story** is a sequence of visualizations that work together to communicate a narrative.

Think of it as a presentation built from Tableau worksheets and dashboards.

### Purpose:
- Explain findings step-by-step
- Guide users through an analysis
- Present insights logically

---

## 5. Why Use Stories? 💡

People often understand and remember information better when it is presented as a story.

Stories help:

- 📚 Explain complex analyses
- 🎯 Highlight important findings
- 📈 Show how insights connect together
- 🗣️ Support business presentations

---

## 6. Story Points 📌

Each page or step within a story is called a:

### 📍 Story Point

A story consists of multiple story points arranged in sequence.

### Example:

#### Story Point 1
📊 Platform Comparison

Compare sales among:
- 🎮 Xbox
- 🎮 PlayStation
- 🎮 Nintendo

---

#### Story Point 2
🔍 PlayStation Deep Dive

Analyze:
- Platform sales
- Product performance
- Trends within the PlayStation ecosystem

---

## 7. Tableau Hierarchy 🪆

A useful way to understand Tableau components is through the concept of **Russian Dolls**.

### Structure:

```text
Workbook
│
├── Worksheets
│
├── Dashboards
│     └── Contain Worksheets
│
└── Stories
      ├── Contain Dashboards
      └── Can also contain Worksheets
```

---

## 8. How Everything Fits Together 🔗

### Level 1: Worksheet 📊

The foundation of Tableau.

Contains:
- Charts
- Graphs
- Maps
- Tables

---

### Level 2: Dashboard 📋

Contains:
- Multiple worksheets

Purpose:
- Combine visualizations
- Create interactive reports

---

### Level 3: Story 📖

Contains:
- Dashboards
- Worksheets (less common)

Purpose:
- Present a narrative
- Guide users through insights

---

## 9. Quick Comparison Table 📑

| Feature | Worksheet 📊 | Dashboard 📋 | Story 📖 |
|----------|-------------|-------------|----------|
| Contains a single visualization | ✅ | ❌ | ❌ |
| Contains multiple visualizations | ❌ | ✅ | ✅ |
| Interactive filtering | Limited | ✅ | ✅ |
| Used for analysis | ✅ | ✅ | ✅ |
| Used for presentations | ⚠️ | ✅ | ✅ |
| Tells a narrative | ❌ | ❌ | ✅ |

---

## 10. Key Takeaways 🎯

### 📊 Worksheet
- Single visualization
- Foundation of Tableau analysis

### 📋 Dashboard
- Collection of worksheets
- Interactive and analytical

### 📖 Story
- Collection of dashboards and/or worksheets
- Used to communicate insights through a narrative

### Remember:

```text
Worksheet
   ↓
Dashboard
   ↓
Story
```

Think of them like Russian dolls 🪆:

📊 Worksheet → inside → 📋 Dashboard → inside → 📖 Story

---

## 11. Let's Practice! 🧠

Now it's time to test your understanding of the differences between:

- 📊 Worksheets
- 📋 Dashboards
- 📖 Stories

Good luck! 🚀
