# 🐼 Pandas, Part 1 📊

## 🎯 Introduction

As a data scientist, you will often work with large amounts of data.

Although datasets can come in many forms, they can frequently be organized into a **tabular structure** similar to a spreadsheet.

A tabular dataset consists of:

- 📋 **Rows** → observations or records
- 📊 **Columns** → variables or features

---

# 📋 Tabular Dataset Examples

## 🌡️ Example 1: Temperature Measurements

Imagine working in a chemical plant where you collect many temperature measurements.

A table might contain:

| Date & Time | Location | Temperature |
|---|---|---:|
| 2025-01-01 08:00 | Plant A | 24.5 |
| 2025-01-01 09:00 | Plant A | 25.1 |
| 2025-01-01 10:00 | Plant B | 26.2 |

Each row represents one **observation**.

Each observation contains several **variables**, such as:

- 📅 Date and time
- 📍 Location
- 🌡️ Temperature

---

## 🌍 Example 2: BRICS Countries

Another example is information about the BRICS countries:

- 🇧🇷 Brazil
- 🇷🇺 Russia
- 🇮🇳 India
- 🇨🇳 China
- 🇿🇦 South Africa

The data can be organized into a table:

| Country | Capital | Area | Population |
|---|---|---:|---:|
| Brazil | Brasília | ... | ... |
| Russia | Moscow | ... | ... |
| India | New Delhi | ... | ... |
| China | Beijing | ... | ... |
| South Africa | Pretoria | ... | ... |

Each row represents a **country** and each column represents a **variable**.

---

# 🧮 Datasets in Python

A 2D NumPy array can represent tabular data because it has:

- Rows
- Columns

However, NumPy arrays are not always the best choice for real-world tabular datasets.

## ⚠️ Problem with NumPy Arrays

NumPy arrays generally work best when all values have the same data type.

For example, in the BRICS dataset:

- `country` → strings
- `capital` → strings
- `area` → floats
- `population` → floats

A dataset can therefore contain **multiple data types**.

NumPy is less convenient for this type of mixed tabular data.

---

# 🐼 Solution: Pandas

**Pandas** is a high-level Python package designed for:

- 📊 Data manipulation
- 🔍 Data analysis
- 🧹 Data cleaning
- 📋 Tabular datasets

Pandas was developed by **Wes McKinney** and is built on top of NumPy.

Compared with NumPy, Pandas provides a higher-level interface specifically suited for working with structured data.

---

# 📑 Pandas DataFrame

In Pandas, tabular data is stored in an object called a:

```text
DataFrame
```

A DataFrame is similar to a spreadsheet or database table.

It contains:

- 📋 Rows → observations
- 📊 Columns → variables
- 🔖 Row labels
- 🏷️ Column labels

Example:

| Index | country | capital | area | population |
|---|---|---|---:|---:|
| BR | Brazil | Brasília | ... | ... |
| RU | Russia | Moscow | ... | ... |
| IN | India | New Delhi | ... | ... |
| CN | China | Beijing | ... | ... |
| SA | South Africa | Pretoria | ... | ... |

Each row can have a unique label such as:

- `BR`
- `RU`
- `IN`
- `CN`
- `SA`

Different columns can also contain different data types.

---

# 📦 Importing Pandas

The standard way to import Pandas is:

```python
import pandas as pd
```

The alias:

```text
pd
```

is the conventional shortcut for Pandas.

---

# 🗂️ Creating a DataFrame from a Dictionary

A DataFrame can be created manually from a dictionary.

Example:

```python
data = {
    'country': ['Brazil', 'Russia', 'India', 'China', 'South Africa'],
    'capital': ['Brasília', 'Moscow', 'New Delhi', 'Beijing', 'Pretoria'],
    'population': [200, 144, 1252, 1357, 52]
}
```

The dictionary structure is:

- 🔑 Keys → column names
- 📋 Values → lists containing the column data

Create the DataFrame using:

```python
brics = pd.DataFrame(data)
```

---

# 🔢 Automatic Row Labels

When a DataFrame is created without specifying row labels, Pandas automatically assigns:

```text
0
1
2
3
4
```

Example:

```python
brics = pd.DataFrame(data)
```

The resulting DataFrame will use numeric indexes by default.

---

# 🏷️ Setting Custom Row Labels

You can manually specify the row labels using the `.index` attribute.

Example:

```python
brics.index = ['BR', 'RU', 'IN', 'CN', 'SA']
```

The DataFrame now uses meaningful country codes as row labels.

Example structure:

| Index | country | capital | population |
|---|---|---|---:|
| BR | Brazil | Brasília | ... |
| RU | Russia | Moscow | ... |
| IN | India | New Delhi | ... |
| CN | China | Beijing | ... |
| SA | South Africa | Pretoria | ... |

---

# 📄 Creating a DataFrame from a CSV File

In real-world data science projects, datasets are usually too large to enter manually.

Instead, data is often stored in an external file.

One common format is:

```text
CSV
```

CSV stands for:

```text
Comma-Separated Values
```

A CSV file might look like:

```text
country,capital,area,population
Brazil,Brasilia,...,...
Russia,Moscow,...,...
India,New Delhi,...,...
China,Beijing,...,...
South Africa,Pretoria,...,...
```

---

# 📥 Importing a CSV File

Pandas provides the:

```python
pd.read_csv()
```

function.

Example:

```python
brics = pd.read_csv('brics.csv')
```

The argument is the path to the CSV file.

---

# ⚠️ Setting the Correct Index Column

Sometimes the CSV file already contains a column intended to be the row index.

For example:

```text
,country,capital,population
BR,Brazil,Brasilia,...
RU,Russia,Moscow,...
IN,India,New Delhi,...
```

If Pandas is not told that the first column contains the index, it may treat that column as a normal data column.

To specify the index column:

```python
brics = pd.read_csv('brics.csv', index_col=0)
```

Here:

```text
index_col=0
```

means:

> Use the first column as the DataFrame index.

---

# 🧩 DataFrame Creation Methods

There are two common ways to create a Pandas DataFrame.

## 1️⃣ From a Dictionary

```python
import pandas as pd

data = {
    'country': ['Brazil', 'Russia', 'India', 'China'],
    'capital': ['Brasilia', 'Moscow', 'New Delhi', 'Beijing']
}

brics = pd.DataFrame(data)
```

---

## 2️⃣ From a CSV File

```python
import pandas as pd

brics = pd.read_csv('brics.csv', index_col=0)
```

The second approach is much more practical when working with large datasets.

---

# 🔍 Important Pandas Concepts

| Concept | Description |
|---|---|
| 🐼 Pandas | Python package for data manipulation and analysis |
| 📑 DataFrame | 2D tabular data structure |
| 🔖 Index | Row labels |
| 🏷️ Columns | Variables in the dataset |
| 📄 CSV | Comma-Separated Values file |
| `pd.DataFrame()` | Creates a DataFrame |
| `pd.read_csv()` | Reads data from a CSV file |
| `index_col` | Specifies the column used as the row index |

---

# 💡 NumPy vs Pandas

| Feature | NumPy | Pandas |
|---|---|---|
| Main structure | `ndarray` | `DataFrame` |
| Best for | Numerical computing | Tabular data analysis |
| Mixed data types | ⚠️ Limited | ✅ Supported |
| Row labels | ❌ No built-in labels | ✅ Yes |
| Column labels | ❌ No built-in labels | ✅ Yes |
| CSV handling | Possible, but less convenient | ✅ Excellent |

---

# 🧠 Key Takeaways

- 🐼 **Pandas** is a high-level package for data manipulation and analysis.
- 📊 A **DataFrame** is Pandas' main structure for tabular datasets.
- 📋 Rows represent observations.
- 📊 Columns represent variables.
- 🔖 DataFrames can have meaningful row labels and column labels.
- 🗂️ DataFrames can be created from dictionaries.
- 📄 Large datasets are commonly imported from CSV files.
- 📥 Use `pd.read_csv()` to load CSV data.
- 🔢 Use `index_col` to specify which CSV column should become the DataFrame index.
- 🚀 Pandas is especially useful when your dataset contains **different data types across columns**.
