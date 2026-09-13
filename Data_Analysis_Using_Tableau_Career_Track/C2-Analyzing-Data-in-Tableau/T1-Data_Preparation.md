# 📊 Data Preparation (Tableau Lesson) — Summary

---

## 🎯 Key Takeaway

Data preparation is a critical step in the analytics process. Before creating visualizations, analysts should:

- Review and clean data fields
- Refine or modify existing fields when necessary
- Create calculated fields to generate additional insights
- Group and summarize data at higher levels
- Identify categorical fields that can be used to analyze data from different perspectives ("slice and dice")

Proper data preparation helps create more meaningful and effective visualizations.

---

## 🚲 Dataset Used: Chicago Divvy Bike Sharing System

The course uses historical trip data from Chicago's Divvy bike-sharing system, focusing on trips from the first half of 2019.

The dataset consists of **two tables**:

### 1. Stations Table
Contains information about bike stations, including:

- Station ID
- Station Name
- Geographic Coordinates
- Number of Available Docks

### 2. Trips Table
Contains individual trip records, including:

- Trip ID
- Bike ID
- Trip Duration (seconds)
- Checkout Time
- Check-in Time
- Starting Station
- Ending Station
- Rider Type (Subscriber or Customer)

Additional subscriber information includes:

- Birth Year
- Gender

---

## 📏 Dimensions vs. Measures

Tableau organizes data into two categories:

### Dimensions
Categorical or qualitative fields used to describe data.

**Examples:**
- Station Name
- Rider Type
- Gender
- Trip ID

### Measures
Numeric fields that can be aggregated.

**Examples:**
- Trip Duration
- Number of Docks

### Important Note

By default, Tableau places numeric fields in the **Measures** section.

However, some numeric fields (such as IDs) should be moved to **Dimensions** because aggregating them (summing or averaging) has no analytical value.

**Example:**
- Trip ID → Dimension ✅
- Station ID → Dimension ✅
- Trip Duration → Measure ✅

---

## ✅ Data Preparation Best Practices

When working with a new dataset:

1. Examine all fields for quality and accuracy.
2. Verify that fields are assigned correctly as Dimensions or Measures.
3. Create calculated fields when additional metrics are needed.
4. Group related values to simplify analysis.
5. Identify fields that can be used to filter, segment, and compare data.
6. Prepare the data before building visualizations.

---

## 📝 Summary

Effective data visualization starts with effective data preparation. In Tableau, analysts should clean and organize data, create useful calculations, identify meaningful categories, and correctly classify fields as Dimensions or Measures. These steps ensure accurate analysis and help reveal insights that may not be visible in traditional reports.
