# 🐼 Pandas Part 2 - Index and Select Data

## 🎯 Introduction

In the previous lesson, we created the **BRICS DataFrame** containing information about Brazil, Russia, India, China, and South Africa.

Example:

| Country | Capital | Area | Population |
|---|---|---|---|
| Brazil | Brasilia | 8.5 | 200.4 |
| Russia | Moscow | 17.1 | 143.5 |
| India | New Delhi | 3.3 | 1252 |
| China | Beijing | 9.6 | 1357 |
| South Africa | Pretoria | 1.2 | 52.98 |

Proper row and column labels make it easier to access and manipulate data inside a DataFrame.

In Pandas, there are several ways to select data:

1. 🔲 Square brackets `[ ]`
2. 🏷️ `loc[]` - label-based selection
3. 🔢 `iloc[]` - position-based selection

---

# 1️⃣ Selecting Columns Using Square Brackets `[ ]`

## Selecting One Column

To select a single column:

```python
brics['country']
```

Example output:

```
BR    Brazil
RU    Russia
IN    India
CN    China
SA    South Africa
Name: country, dtype: object
```

The result is a:

```
Pandas Series
```

A Series is a one-dimensional labeled array.

---

## Checking the Type

You can check the returned object using:

```python
type(brics['country'])
```

Output:

```
pandas.core.series.Series
```

---

# Selecting One Column as a DataFrame

If you want to keep the result as a DataFrame, use double square brackets:

```python
brics[['country']]
```

Output:

| | country |
|-|-|
| BR | Brazil |
| RU | Russia |
| IN | India |
| CN | China |
| SA | South Africa |

The result remains a DataFrame.

---

# Selecting Multiple Columns

You can select multiple columns by placing a list inside the brackets:

```python
brics[['country', 'capital']]
```

Output:

| | country | capital |
|-|-|-|
| BR | Brazil | Brasilia |
| RU | Russia | Moscow |
| IN | India | New Delhi |
| CN | China | Beijing |
| SA | South Africa | Pretoria |

---

# 2️⃣ Selecting Rows Using Square Brackets

Square brackets can also select rows using slicing.

Example:

```python
brics[1:4]
```

This selects:

- Row index 1
- Row index 2
- Row index 3

Remember:

- Python indexing starts at `0`
- The ending value is excluded

Example:

```
1:4
```

means:

```
1, 2, 3
```

---

# ⚠️ Limitation of Square Brackets

Square brackets work, but they have limitations.

With NumPy arrays, you can do:

```python
array[row, column]
```

However, regular DataFrame brackets cannot easily select both rows and columns together.

For more powerful selection, Pandas provides:

- `loc[]`
- `iloc[]`

---

# 3️⃣ Label-Based Selection with `loc[]`

`loc[]` selects data using row and column labels.

Syntax:

```python
dataframe.loc[row_label, column_label]
```

---

# Selecting a Row Using `loc`

Example:

```python
brics.loc['RU']
```

This selects the Russia row.

Output:

```
country       Russia
capital       Moscow
area          17.1
population    143.5
```

The result is a Series.

---

# Selecting a Row as a DataFrame

Use double brackets:

```python
brics.loc[['RU']]
```

Output:

| | country | capital |
|-|-|-|
| RU | Russia | Moscow |

---

# Selecting Multiple Rows

Use a list of row labels:

```python
brics.loc[['RU', 'IN', 'CN']]
```

This selects:

- Russia
- India
- China

---

# Selecting Rows and Columns with `loc`

`loc` allows selecting rows and columns at the same time.

Syntax:

```python
brics.loc[row_labels, column_labels]
```

Example:

```python
brics.loc[['RU', 'IN', 'CN'], ['country', 'capital']]
```

Output:

| | country | capital |
|-|-|-|
| RU | Russia | Moscow |
| IN | India | New Delhi |
| CN | China | Beijing |

---

# Selecting All Rows with Specific Columns

Use `:` to select all rows:

```python
brics.loc[:, ['country', 'capital']]
```

Meaning:

```
All rows
Only country and capital columns
```

---

# 4️⃣ Position-Based Selection with `iloc[]`

`iloc[]` works like NumPy indexing.

Instead of labels, it uses row and column positions.

Syntax:

```python
dataframe.iloc[row_position, column_position]
```

---

# Selecting a Row Using `iloc`

Using `loc`:

```python
brics.loc[['RU']]
```

Using `iloc`:

```python
brics.iloc[[1]]
```

Both return the Russia row.

Why?

Because Russia is located at index position:

```
1
```

---

# Selecting Multiple Rows Using `iloc`

Example:

```python
brics.iloc[[1,2,3]]
```

Selects:

| Position | Country |
|-|-|
| 1 | Russia |
| 2 | India |
| 3 | China |

---

# Selecting Rows and Columns Using `iloc`

Example:

```python
brics.iloc[[1,2,3],[0,1]]
```

Meaning:

Rows:

```
1, 2, 3
```

Columns:

```
0, 1
```

Result:

| | country | capital |
|-|-|-|
| RU | Russia | Moscow |
| IN | India | New Delhi |
| CN | China | Beijing |

---

# Selecting All Rows and Specific Columns with `iloc`

Example:

```python
brics.iloc[:, [0,1]]
```

Meaning:

```
All rows
Columns 0 and 1
```

---

# 🆚 loc vs iloc

| Feature | `loc[]` | `iloc[]` |
|-|-|-|
| Selection type | Label-based | Position-based |
| Uses | Row/column names | Row/column numbers |
| Example row selection | `brics.loc['RU']` | `brics.iloc[1]` |
| Similar to | Dictionary lookup | NumPy indexing |

---

# 📌 Summary

## 🔲 Square Brackets

Use for simple selections:

```python
brics['country']
```

Select columns.

```python
brics[1:4]
```

Select rows using slicing.

---

## 🏷️ loc[]

Use labels:

```python
brics.loc['RU']
```

Select by row name.

```python
brics.loc[['RU'], ['country']]
```

Select rows and columns using labels.

---

## 🔢 iloc[]

Use positions:

```python
brics.iloc[1]
```

Select by row number.

```python
brics.iloc[[1,2],[0,1]]
```

Select rows and columns using positions.

---

# 🧠 Key Takeaways

✅ Pandas provides multiple ways to access DataFrame data.  
✅ Square brackets are useful for simple column and row selection.  
✅ `loc[]` selects data using labels.  
✅ `iloc[]` selects data using integer positions.  
✅ `loc[]` and `iloc[]` make Pandas selection similar to NumPy indexing.  
✅ Understanding indexing is essential for efficient data analysis with Pandas. 🐼📊
