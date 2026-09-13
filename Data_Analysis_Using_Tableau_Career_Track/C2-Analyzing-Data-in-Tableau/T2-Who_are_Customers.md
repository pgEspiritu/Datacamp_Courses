# 👥 Who Are Your Customers? (Tableau Lesson) — Summary

---

## 🎯 Key Takeaway

Understanding **who your customers are** is a fundamental step in data analysis. Customer demographics and user classifications help analysts identify behavior patterns, segment users, and create more meaningful visualizations.

In Tableau, customer-related fields can be used to **slice and dice** data, revealing insights about different groups of users.

---

## 🚲 Customer Information in the Divvy Dataset

The Divvy Trips Table contains several fields that help describe customers:

| Field | Purpose |
|---------|---------|
| Usertype | Identifies rider category |
| Gender | Provides demographic information |
| Birthyear | Helps estimate rider age groups |

These fields allow analysts to explore who is using the bike-sharing service.

---

## 🚴 User Types

### Subscribers

Subscribers are riders who maintain an ongoing relationship with Divvy.

**Characteristics:**
- Often commuters
- Purchase subscriptions
- Provide personal information during registration

**Available Data:**
- Gender
- Birthyear

---

### 🚴‍♀️ Customers (Non-Subscribers)

Customers are riders who use the service occasionally.

**Characteristics:**
- Often tourists or casual riders
- No ongoing relationship with Divvy
- Usually purchase short-term passes

**Available Data:**
- Gender often missing
- Birthyear often missing

In Tableau, these missing values appear as **Null**.

---

## 📌 Important Note About Customer Data

Some riders may have previously been subscribers and later switched to customer status.

As a result:

- Existing Gender information may remain in the dataset
- Existing Birthyear information may remain in the dataset

Therefore, not all customer records have missing demographic data.

---

## 🔍 Understanding Missing Values

Missing values are not always data quality issues.

Before replacing or removing missing values, analysts should understand **why** the information is missing.

In the Divvy dataset:

- Customers are generally not required to provide demographic information.
- Therefore, missing Gender and Birthyear values are expected.

Understanding the reason behind missing data helps improve analysis accuracy.

---

## 🏷️ Replacing Null Values

Since the cause of missing values is known, Tableau can be used to replace Null values with a more meaningful label.

### Original Value
- Null

### Suggested Label
- **Day Pass Riders**

This label indicates:

- No ongoing relationship with Divvy
- Typically purchased a short-term pass
- Demographic information was not collected

Using descriptive labels improves dashboard readability and interpretation.

---

## 📊 Benefits of Customer Analysis

Analyzing customer-related fields helps:

- Identify major customer segments
- Understand rider demographics
- Compare subscribers and non-subscribers
- Discover usage patterns
- Improve customer engagement strategies

---

## 📈 Tableau Analysis Strategy

Use customer fields such as:

- Usertype
- Gender
- Birthyear

to:

1. Segment riders into meaningful groups.
2. Compare behavior across customer types.
3. Analyze demographic trends.
4. Explore age and gender distributions.
5. Uncover patterns in customer behavior.

---

## ✅ Best Practices

- Investigate "Who" before performing deeper analysis.
- Understand the reason behind missing values.
- Avoid treating all Null values as errors.
- Replace known Null categories with meaningful labels.
- Use demographic fields to enrich visualizations and storytelling.

---

## 📝 Summary

Customer analysis begins with understanding who uses a service. In the Divvy dataset, fields such as Usertype, Gender, and Birthyear provide valuable insights into rider demographics and behavior. By properly handling missing values and segmenting customers into meaningful groups, Tableau users can create clearer visualizations and uncover deeper business insights.
