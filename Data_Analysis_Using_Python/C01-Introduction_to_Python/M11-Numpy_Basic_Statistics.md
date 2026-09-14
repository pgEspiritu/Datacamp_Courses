# 🔢 NumPy: Basic Statistics 📊

## 1. 📌 Overview

A typical first step in analyzing data is **getting to know your data**.

For small NumPy arrays, it is easy to inspect the values manually. However, as a data scientist 👨‍💻, you will often work with thousands, millions, or even billions of numbers.

To understand large datasets, you need statistical tools that can summarize and describe the data efficiently.

---

# 2. 🔍 Data Analysis with NumPy

When working with large datasets, simply looking at raw values is not enough to gain meaningful insights.

For example, imagine conducting a city-wide survey 🏙️ where you ask **5,000 adults** about their height and weight.

The collected information can be stored in a 2D NumPy array called `np_city`.

Structure:

- 👤 Rows → represent individual people
- 📏 Columns → represent measurements such as height and weight

Example:

    np_city =
    [
        [height_1, weight_1],
        [height_2, weight_2],
        [height_3, weight_3],
        ...
    ]

Instead of manually examining thousands of numbers, NumPy provides statistical functions 📈 that summarize the dataset.

---

# 3. 📊 Mean (Average)

The **mean** calculates the average value of a dataset.

NumPy provides the `np.mean()` function.

Example:

    import numpy as np

    average_height = np.mean(np_city[:, 0])

    print(average_height)

Explanation:

- `np_city[:, 0]` selects all rows from the first column.
- The first column contains height values 📏.
- `np.mean()` calculates the average height.

Example result:

    1.75

This means the average height of the surveyed population is approximately **1.75 meters**.

---

# 4. 📍 Median

The **median** is the middle value of a dataset after sorting all values from smallest to largest.

NumPy provides the `np.median()` function.

Example:

    median_height = np.median(np_city[:, 0])

    print(median_height)

The median is useful because it is less affected by extreme values or outliers ⚠️.

Example:

Dataset:

    [150, 160, 170, 180, 250]

Mean:

    182

Median:

    170

The median can provide a better representation of the typical value.

---

# 5. 📈 Statistical Functions in NumPy

NumPy provides several functions for analyzing and understanding datasets.

## 🔗 Correlation

The `np.corrcoef()` function measures the relationship between variables.

Example:

    np.corrcoef(np_city[:, 0], np_city[:, 1])

This can help determine whether variables such as height and weight are related.

Example:

- 📏 Height increases while ⚖️ weight increases → positive correlation
- 📏 Height increases while ⚖️ weight decreases → negative correlation

---

## 📉 Standard Deviation

The `np.std()` function measures how spread out values are from the average.

Example:

    np.std(np_city[:, 0])

Interpretation:

- ✅ Low standard deviation → values are close to the average
- ⚠️ High standard deviation → values are more spread out

---

## ➕ Sum

The `np.sum()` function calculates the total of values.

Example:

    np.sum(np_city[:, 1])

This can calculate the total weight of all participants.

---

## 🔄 Sort

The `np.sort()` function arranges values in ascending order.

Example:

    np.sort(np_city[:, 0])

Example output:

    [1.55, 1.60, 1.68, 1.75, 1.82]

---

# 6. ⚡ Why Use NumPy for Statistics?

Python includes built-in functions for some calculations, but NumPy is optimized for numerical analysis.

Advantages of NumPy:

- 🚀 Faster calculations
- 🧮 Optimized numerical operations
- 📦 Efficient storage using a single data type
- 🔢 Ability to perform operations on entire arrays

Example:

    np.mean(array)

is faster and more efficient than manually calculating averages using loops.

---

# 7. 🎲 Generating Data with NumPy

NumPy can also generate datasets using random functions.

Example:

    height = np.random.normal(1.75, 0.10, 5000)

    weight = np.random.normal(70, 15, 5000)

This creates simulated height and weight measurements.

The arrays can then be combined into a 2D array using `np.column_stack()`.

Example:

    np_city = np.column_stack((height, weight))

Result:

    [
        [height_1, weight_1],
        [height_2, weight_2],
        [height_3, weight_3]
    ]

---

# 🧠 Key Takeaways

- 🔢 NumPy provides powerful tools for analyzing large datasets.
- 📊 Statistical functions help summarize and understand data.
- ⚡ NumPy is optimized for fast numerical calculations.
- 📈 Common NumPy statistical functions include:

| Function | Purpose |
|---|---|
| `np.mean()` | 📊 Calculate average |
| `np.median()` | 📍 Find middle value |
| `np.std()` | 📉 Calculate standard deviation |
| `np.corrcoef()` | 🔗 Measure correlation |
| `np.sum()` | ➕ Calculate total |
| `np.sort()` | 🔄 Sort values |

NumPy is an essential Python library for **data science, analytics, and machine learning workflows** 🚀🐍.
