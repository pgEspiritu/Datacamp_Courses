# 📅 Working with Dates in Tableau

---

## 1. Working with Dates 📆

Dates are one of the most common data types used in analysis.

Many business questions depend on understanding **when** something happened.

### Examples:
- 📅 When did an event occur?
- 📈 How has a metric changed over time?
- 🌦️ Are there seasonal trends?
- 📊 What patterns emerge across months, quarters, or years?

Fortunately, Tableau makes date analysis simple and powerful.

---

## 2. Date Data in Tableau 📂

When Tableau detects a date field, it automatically:

- Places it in the **Dimensions** area of the Data Pane
- Assigns it a **Date icon** 📅

### Example:
The **Date** field from the UN dataset is recognized automatically as a date dimension.

📌 Dates are typically treated as dimensions because they help organize and segment data over time.

---

## 3. Date Hierarchy 🌳

One of Tableau's most useful features is its built-in **Date Hierarchy**.

This allows you to drill down into different levels of time.

### Hierarchy Levels:

```text
Year
 └── Quarter
      └── Month
           └── Day
```

### Example:

```text
2025
 └── Q2
      └── June
           └── 02
```

---

## 4. Drilling Down Through Dates 🔍

Using the date hierarchy, you can:

### Start with a high-level view:
- 📅 Year

Then drill down to:
- 📊 Quarter
- 📆 Month
- 📍 Day

This makes it easy to move between summary and detailed views of your data.

---

## 5. Why Date Analysis Matters 📈

Dates help reveal patterns that may not be visible otherwise.

### Common Insights:
- 🌦️ Seasonality
- 📈 Growth trends
- 📉 Declines over time
- 🎯 Peak periods
- 📊 Cyclical behavior

Analyzing data over time helps organizations make better decisions and allocate resources effectively.

---

## 6. Business Context 🏥

You are working for the:

🏥 :contentReference[oaicite:0]{index=0}

The organization wants to understand birth patterns using historical data.

---

## 7. Business Question ❓

The key question is:

> **Is there seasonality in the number of births in Chile?**

If seasonality exists:

> **During which month are the fewest babies typically born?**

---

## 8. Why This Question Matters 👶

Understanding birth trends helps the World Health Organization:

- 🏥 Plan newborn healthcare services
- 👩‍⚕️ Allocate medical personnel
- 🚑 Prepare healthcare facilities
- 📦 Distribute medical resources efficiently
- 📈 Anticipate periods of high and low demand

This ensures adequate newborn care throughout the year.

---

## 9. Expected Outcome 🎯

By the end of this lesson, you will be able to create a visualization that:

- 📊 Identifies seasonal birth patterns
- 📅 Compares births by month
- 🔍 Reveals months with the highest and lowest birth rates
- 🏥 Supports healthcare planning decisions

---

## 10. Let's Practice! 🧠

Before answering the business question for Chile 🇨🇱, you will first perform a similar date analysis using data from Portugal 🇵🇹.

This will help you become familiar with:
- 📅 Date hierarchies
- 📊 Time-series visualizations
- 🔍 Seasonal trend analysis in Tableau
