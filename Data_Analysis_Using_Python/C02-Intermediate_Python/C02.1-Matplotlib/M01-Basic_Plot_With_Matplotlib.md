# 📊 Basic Plots with Matplotlib

## 🎯 Introduction

Hi! My name is Hugo, and I'm a data scientist and educator at DataCamp. In this chapter, you will take your Python skills to the next level, especially for **data science applications**.

You will learn how to:

- 📈 Visualize data using Python
- 🗂️ Store data in new data structures
- 🔄 Use control structures to customize the flow of scripts and algorithms
- 🧪 Apply these skills in a case study to solve a real-world challenge

---

# 📌 Data Visualization

Data visualization is an important part of data analysis.

It helps you:

- 🔍 Explore datasets and understand patterns
- 💡 Discover insights hidden in data
- 📢 Communicate findings effectively to others

A good visualization allows data to tell its own story.

---

# 🌍 Example: Beautiful Data Visualization

One famous example of effective data visualization comes from the late Swedish professor **Hans Rosling**.

His global development presentations became popular because of the way he used beautiful and interactive visualizations to explain complex datasets.

The visualization shown is a **bubble chart**, where:

- 🟢 Each bubble represents a country
- 📏 The size of the bubble represents the country's population
- 🇨🇳 China and 🇮🇳 India appear as the largest bubbles because they have the biggest populations

Source:
- Gapminder, *Wealth and Health of Nations*

---

## 📊 Understanding the Axes

The bubble chart contains two axes:

### Horizontal Axis (X-axis)

Represents:

```
GDP per capita
```

Measured in:

```
US dollars
```

### Vertical Axis (Y-axis)

Represents:

```
Life expectancy
```

---

## 🔎 Insights from the Visualization

The chart shows:

- Countries with higher GDP per capita generally have higher life expectancy.
- However, countries with similar income levels can still have significant differences in life expectancy.

This demonstrates how visualization can reveal patterns that are difficult to see from raw numbers.

By the end of this chapter, you will be able to create similar visualizations yourself! 🚀

---

# 🐍 Matplotlib

There are many visualization packages available in Python, but one of the most important and widely used is:

```
Matplotlib
```

Matplotlib is the foundation of many Python visualization tools.

For data visualization, you will mainly use the:

```
matplotlib.pyplot
```

subpackage.

By convention, it is imported using the alias:

```python
import matplotlib.pyplot as plt
```

---

# 📈 Creating a Line Plot

Suppose we want to visualize the growth of the world population.

We have two lists:

```python
year
```

Contains the years.

Example:

```python
1970
```

represents the year.

---

```python
pop
```

Contains the corresponding population values.

Example:

```
3.7 billion people in 1970
```

---

## Creating the Plot

To create a line chart:

```python
plt.plot(year, pop)
```

The arguments represent:

| Argument | Purpose |
|---|---|
| First argument | Horizontal axis (X-axis) |
| Second argument | Vertical axis (Y-axis) |

---

## Displaying the Plot

Calling:

```python
plt.plot()
```

does not immediately display the visualization.

Matplotlib waits because you may want to customize the chart first.

To display the chart:

```python
plt.show()
```

---

## Example

```python
import matplotlib.pyplot as plt

plt.plot(year, pop)

plt.show()
```

---

# 📉 Understanding a Line Plot

A line chart shows:

- 📅 Years on the horizontal axis
- 👥 Population values on the vertical axis
- 🔗 Lines connecting data points

Example insight:

```
1950 → Around 2.5 billion people

2010 → Around 7 billion people
```

The world population almost tripled within 60 years.

---

# 🔵 Scatter Plot

Another important visualization type is the:

```
Scatter plot
```

A scatter plot displays individual data points without connecting them with lines.

---

## Creating a Scatter Plot

Instead of:

```python
plt.plot(year, pop)
```

Use:

```python
plt.scatter(year, pop)
```

---

## Difference Between Line Plot and Scatter Plot

| Plot Type | Purpose |
|---|---|
| Line Plot 📈 | Shows trends and changes over time |
| Scatter Plot 🔵 | Shows individual observations and relationships |

---

## Why Use Scatter Plots?

Scatter plots are often better when:

- You want to examine relationships between variables
- You want to see individual observations
- You want a more honest representation of limited data points

A scatter plot makes it clear that the visualization is based on individual measurements.

---

# 📝 Key Takeaways

✅ Data visualization helps explore and communicate insights  
✅ Matplotlib is one of Python's most important visualization libraries  
✅ `matplotlib.pyplot` is commonly imported as `plt`  
✅ `plt.plot()` creates line charts  
✅ `plt.scatter()` creates scatter plots  
✅ `plt.show()` displays the visualization  
✅ Line plots are useful for trends over time  
✅ Scatter plots are useful for relationships between variables  

---

# 🚀 Let's Practice!

Now that you understand the basics of Matplotlib, you can start creating your own visualizations and uncover insights from data! 📊
