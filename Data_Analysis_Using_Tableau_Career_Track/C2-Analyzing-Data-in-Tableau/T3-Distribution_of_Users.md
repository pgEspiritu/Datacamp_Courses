# 📊 The Distribution of Users (Tableau Lesson) — Summary

---

## 🎯 Key Takeaway

In addition to **Usertype** and **Gender**, **Birthyear** provides another valuable demographic attribute that can be used to calculate a user's **Age**.

Analyzing age distribution helps organizations understand which age groups use their services most frequently, enabling more effective marketing, customer engagement, and business decision-making.

---

## 👥 Demographic Fields in the Divvy Dataset

The customer demographics analyzed in the Divvy dataset include:

- Usertype
- Gender
- Birthyear

### Calculated Field

From **Birthyear**, analysts can create a calculated field:

**Age = Current Year − Birthyear**

This allows age-based analysis and visualization.

---

## 🎯 Why Age Analysis Matters

Understanding user age distribution helps organizations:

- Identify primary customer segments
- Develop targeted marketing campaigns
- Improve customer engagement
- Tailor products and services to specific demographics
- Optimize advertising investments
- Discover new market opportunities

By knowing which age groups generate the most rides, Divvy can focus marketing efforts on users most likely to engage with the service.

---

## 📈 Using Histograms to Analyze Age Distribution

Since **Age** is a numerical field, it is best visualized using a **Histogram**.

### What Is a Histogram?

A histogram is a chart that groups numerical values into ranges and displays the frequency of observations within each range.

For Divvy:

- Each bar represents an age range.
- The height of the bar represents the number of rides taken by users within that age range.

---

## 📦 Understanding Bins

A **bin** is a range of values grouped together in a histogram.

### Example: 3-Year Bins

| Bin Range | Included Ages |
|------------|--------------|
| 27–29 | 27, 28, 29 |
| 30–32 | 30, 31, 32 |
| 33–35 | 33, 34, 35 |

The height of each bar shows the total rides associated with users in that age range.

### Interpretation

- Taller bars indicate higher ride activity.
- Shorter bars indicate lower ride activity.
- The tallest bar identifies the age group responsible for the most trips.

---

## ⚖️ Choosing the Right Bin Size

The size of a bin significantly affects how data is displayed and interpreted.

### Large Bins (e.g., 3 Years)

#### Advantages
- Reduces visual clutter
- Makes trends easier to identify
- Produces a smoother distribution

#### Disadvantages
- Hides detailed patterns
- May mask important variations between ages

---

### Small Bins (e.g., 1 Year)

#### Advantages
- Provides greater detail
- Displays activity for individual ages
- Reveals subtle patterns

#### Disadvantages
- Creates more visual noise
- Makes charts appear less smooth
- Can make trends harder to identify

---

## 🔍 Finding the Optimal Bin Size

There is no universally correct bin size.

Analysts should experiment with different sizes to find the most useful view of the data.

A good bin size should:

- Highlight meaningful patterns
- Preserve important details
- Minimize unnecessary noise
- Be easy for viewers to interpret

---

## 💼 Business Value of Age Distribution Analysis

Age distribution analysis helps Divvy:

- Identify its most active users
- Understand customer demographics
- Improve marketing effectiveness
- Target advertising toward likely riders
- Increase customer acquisition opportunities
- Allocate marketing resources more efficiently

These insights support data-driven business and marketing decisions.

---

## 📊 Histogram Bin Comparison

| Bin Size | Advantages | Disadvantages |
|-----------|-----------|--------------|
| 3-Year Bins | Less noise, easier trend identification | Less detail |
| 1-Year Bins | More detail, precise analysis | More noise and fluctuations |

---

## ✅ Best Practices

- Create an Age field from Birthyear.
- Use histograms for numerical distributions.
- Experiment with multiple bin sizes.
- Balance detail and readability.
- Focus on identifying meaningful customer segments.
- Use age insights to support marketing and business strategies.

---

## 📝 Summary

Age is a powerful demographic variable derived from Birthyear. Because age is numerical, Tableau users typically analyze it using histograms, which group values into bins. Selecting an appropriate bin size is important because larger bins emphasize overall trends while smaller bins provide greater detail. Understanding age distribution helps organizations identify key customer groups, improve marketing efforts, and make more informed business decisions.
