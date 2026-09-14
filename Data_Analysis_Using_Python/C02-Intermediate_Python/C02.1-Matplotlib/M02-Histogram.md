# 📊 Histogram - Matplotlib

## 🎯 Introduction

You are doing great! 🚀

In this lesson, we will learn about another important visualization tool:

```
Histogram
```

A histogram is a type of chart that helps us understand the **distribution of data**.

It allows data scientists to quickly see:

- Where most values are concentrated
- How data is spread out
- Whether there are unusual patterns or outliers

---

# 📌 What is a Histogram?

A histogram groups numerical data into ranges called:

```
Bins
```

Each bin represents a range of values.

The height of each bar shows:

```
Number of data points inside the bin
```

---

# 🧮 Example of Histogram Creation

Imagine we have 12 values between:

```
0 and 6
```

Example:

```
[0.5, 1.2, 1.8, 2.1, 2.5, 3.0, 3.2, 3.8, 4.1, 4.5, 5.0, 5.5]
```

To create a histogram:

## Step 1: Divide Data into Bins

Example:

```
3 bins
```

Each bin has a width of:

```
2
```

The ranges become:

```
Bin 1 → 0 to 2
Bin 2 → 2 to 4
Bin 3 → 4 to 6
```

---

## Step 2: Count Values in Each Bin

Example:

| Bin | Range | Number of Values |
|---|---|---|
| Bin 1 | 0 - 2 | 4 |
| Bin 2 | 2 - 4 | 6 |
| Bin 3 | 4 - 6 | 2 |

---

## Step 3: Draw the Histogram

Each bar represents one bin.

The height represents:

```
Frequency
```

or:

```
Number of observations
```

---

# 📊 Why Use Histograms?

Histograms help answer questions like:

- What is the most common value range?
- Is the data evenly distributed?
- Are there extreme values?
- Is the data skewed?

Example:

If most values appear in the middle:

```
      █
    █ █ █
  █ █ █ █ █
```

The dataset is concentrated around average values.

---

# 🐍 Creating Histograms with Matplotlib

Matplotlib provides the:

```python
plt.hist()
```

function.

Basic structure:

```python
import matplotlib.pyplot as plt

plt.hist(values, bins)

plt.show()
```

---

# 📌 Matplotlib Histogram Syntax

Example:

```python
plt.hist(values, bins=3)

plt.show()
```

Parameters:

| Parameter | Description |
|---|---|
| `values` | Data used to create the histogram |
| `bins` | Number of groups/ranges |
| `plt.show()` | Displays the chart |

---

# 🔍 Understanding the `bins` Parameter

The `bins` argument controls how data is divided.

Example:

```python
plt.hist(data, bins=5)
```

creates:

```
5 groups
```

If the `bins` argument is not provided:

```python
plt.hist(data)
```

Matplotlib automatically uses:

```
10 bins (default)
```

---

# 💡 Matplotlib Histogram Example

```python
# Import matplotlib
import matplotlib.pyplot as plt

# Create sample data
values = [0.5, 1.2, 1.8, 2.1, 2.5, 
          3.0, 3.2, 3.8, 4.1, 4.5,
          5.0, 5.5]

# Create histogram
plt.hist(values, bins=3)

# Display plot
plt.show()
```

---

# 📈 Histogram Interpretation

The histogram provides a quick overview of the data distribution.

Example observations:

- Most values are located in the middle range.
- Fewer values appear at the extreme ends.
- The shape of the histogram reveals the structure of the dataset.

---

# 🌍 Real-World Example: Population Pyramid

Histograms can also be used to visualize demographic information.

A population pyramid shows:

- Age distribution
- Male population
- Female population

Example:

```
Age
90+
80-89
70-79
60-69
50-59
40-49
30-39
20-29
10-19
0-9
```

The bars represent population size per age group.

---

# 👥 Population Changes Over Time

Population pyramids can compare different years.

Example:

## Year 2010

- Large population in the 40-44 age group
- Represents the baby boomer generation

## Year 2050

- Population distribution becomes flatter
- Older age groups increase

Histograms make demographic changes easier to understand visually.

---

# 📝 Key Takeaways

✅ Histograms show the distribution of numerical data.  
✅ Data is grouped into ranges called bins.  
✅ The height of each bar represents frequency.  
✅ `plt.hist()` creates histograms in Matplotlib.  
✅ The `bins` parameter controls the number of groups.  
✅ Histograms are useful for finding patterns, trends, and outliers. 📊

---

# 🚀 Practice Goal

Use histograms to explore datasets and understand how values are distributed.

Visualization helps transform raw numbers into meaningful insights! 🔍📈
