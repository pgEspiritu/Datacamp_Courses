# 🧮 Calculated Fields in Tableau

---

## 1. Calculated Fields ✨  
Now that you've mastered the basics of filtering and sorting, it's time to learn about **Calculated Fields**.

Calculated fields are one of Tableau's most powerful features because they allow you to create new data from existing data.

---

## 2. What Are Calculated Fields? 🤔  
According to Tableau:

> Calculated fields allow you to create new data from data that already exists in your data source.

### 📌 What does this mean?
A calculated field creates a new column based on existing columns using formulas and functions.

### 💡 Why use calculated fields?
- Create new metrics
- Transform existing data
- Simplify analysis
- Build custom business calculations

⚠️ Important: Calculated fields do **not** modify the original data source.

---

## 3. Examples of Calculated Fields 📊

### 💱 Currency Conversion
Suppose your sales data is in US Dollars (USD), but you need values in Euros (EUR).

You can create a calculated field:

```text
Sales (EUR) = Sales (USD) × Exchange Rate
```

Example:

```text
Sales (EUR) = Sales (USD) × 0.9
```

---

### ⛽ Rounding Gas Prices
You may want to round prices up to the nearest whole number.

Example:

```text
ROUND(Gas Price)
```

---

### 📧 Email Classification
Create a field that identifies whether an email address belongs to Gmail.

Example output:

| Email | Gmail Account? |
|---------|---------|
| user@gmail.com | Yes |
| user@yahoo.com | No |

---

## 4. More Examples of Calculated Fields 📈

### 📅 Extracting the Year
Suppose you have a full date field:

```text
2025-06-02
```

You can create a new field containing only:

```text
2025
```

This is useful when:
- Grouping by year
- Creating yearly reports
- Comparing annual trends

---

### 💹 Price-to-Earnings Ratio (P/E Ratio)
Calculated fields can use multiple columns.

Example:

```text
Price Earnings Ratio = Stock Price / Earnings Per Share
```

This combines two existing fields to create a new business metric.

---

## 5. Key Characteristics of Calculated Fields 🔑

When you create a calculated field:

### ✅ Tableau Creates:
- A new column
- A new field in your workbook

### ✅ The Field Can Be:
- 📂 A Dimension
- 📏 A Measure

### ✅ Tableau Does NOT:
- Modify the original dataset
- Change the underlying data source

Think of calculated fields as **virtual columns** created inside Tableau.

---

## 6. Functions in Calculated Fields ⚙️

Calculated fields are built using **functions**.

Functions typically use:

```text
FUNCTION_NAME(argument)
```

### Example:

```text
ROUND(Price)
```

Where:
- `ROUND` = function
- `Price` = argument

---

## 7. Types of Functions 🛠️

Tableau provides many function categories:

- 🔢 Number Functions
- 📅 Date Functions
- 📝 String Functions
- 🧠 Logical Functions
- 📊 Aggregate Functions
- 🌐 Spatial Functions

### 📌 In this chapter:
We focus only on **Number Functions**.

---

## 8. Dataset Used 🌍📚

In the upcoming demonstrations, we will use a new **Gapminder** indicator:

### 🎓 Mean Years in School

Definition:

> The average number of years spent in school, from primary education through graduate studies.

---

### Why is it Important?
This indicator helps measure:

- 📚 Educational attainment
- 👥 Social development
- 💼 Economic development

---

### Dataset Structure

The dataset contains:

- 🌍 Country
- 📅 Year
- 👨 Male demographics
- 👩 Female demographics

The education indicator is divided by:

### 👥 Gender
- Male
- Female

### 🎂 Age Groups
- Five age categories

This results in:

📊 **10 demographic columns** for Mean Years in School.

---

## 9. Let’s Practice! 🧠

Now it's time to create your own calculated fields in Tableau and see how powerful custom calculations can be!
