# 🐍 Variables and Types

## 📦 Variables

A **variable** is a named location used to store a value.

You create a variable using the assignment operator `=`.

```python
height = 1.79
weight = 68.7
```

You can retrieve the stored value by using the variable's name:

```python
height
```

Output:

```text
1.79
```

### 🔑 Important

* 🏷️ Variables have names.
* 🔤 Variable names are **case-sensitive**.
* 💾 Variables store values.
* 🔄 Variables can be changed during a program.
* ♻️ Using variables makes code easier to reuse and reproduce.

---

# ⚖️ Calculating BMI

BMI can be calculated using:

```text
BMI = weight / height²
```

In Python:

```python
height = 1.79
weight = 68.7

bmi = weight / height ** 2
```

The result is stored in the variable `bmi`.

```python
bmi
```

### 💡 Why Use Variables?

Instead of writing the actual values repeatedly, you can use variables:

```python
bmi = weight / height ** 2
```

If the weight changes:

```python
weight = 75
```

you can rerun the calculation:

```python
bmi = weight / height ** 2
```

The BMI automatically updates based on the new weight.

> ♻️ **Variables help make code reusable and reproducible.**

---

# 🔢 Python Data Types

Every value in Python has a **data type**.

You can check a value's type using the `type()` function:

```python
type(bmi)
```

---

## 🔢 `int` — Integer

An **integer** is a whole number without a decimal part.

```python
age = 25
type(age)
```

Output:

```text
int
```

Examples:

```python
10
0
-5
100
```

---

## 🔢 `float` — Floating-Point Number

A **float** represents a number that can contain a fractional/decimal part.

```python
height = 1.79
type(height)
```

Output:

```text
float
```

Examples:

```python
3.14
1.79
68.7
-2.5
```

---

## 🔤 `str` — String

A **string** represents text.

Strings can be created using either single or double quotation marks:

```python
name = "Gio"
```

or:

```python
name = 'Gio'
```

Check its type:

```python
type(name)
```

Output:

```text
str
```

### 💡 Examples

```python
"Hello"
'Python'
"Data Science"
```

---

## ✅ `bool` — Boolean

A **Boolean** represents one of two possible values:

* `True`
* `False`

Example:

```python
is_student = True
```

or:

```python
is_complete = False
```

Boolean values are especially useful for:

* 🔍 Filtering data
* ✅ Conditions
* 🔀 Decision-making
* 📊 Data analysis

---

# ➕ Operators Can Behave Differently

Python operators can behave differently depending on the **data type** being used.

### 🔢 Adding Integers

```python
4 + 5
```

Output:

```text
9
```

Python performs numerical addition.

### 🔤 Adding Strings

```python
"Data" + "Camp"
```

Output:

```text
DataCamp
```

Python **concatenates** (joins) the strings.

### 🧠 Key Principle

> 💡 **How Python behaves depends on the data types you're working with.**

The same `+` operator can perform different operations:

| Data Type   | Operation         | Result       |
| ----------- | ----------------- | ------------ |
| 🔢 Integers | `4 + 5`           | `9`          |
| 🔤 Strings  | `"Data" + "Camp"` | `"DataCamp"` |

---

# 🧠 Key Takeaways

| Concept                | Description                                    |
| ---------------------- | ---------------------------------------------- |
| 📦 **Variable**        | Named storage for a value                      |
| `=`                    | Assignment operator                            |
| 🔢 **int**             | Whole number                                   |
| 🔢 **float**           | Decimal/floating-point number                  |
| 🔤 **str**             | Text/string                                    |
| ✅ **bool**             | `True` or `False`                              |
| `type()`               | Checks the data type of a value                |
| ➕ `+`                  | Behavior depends on the data type              |
| ♻️ **Reproducibility** | Variables make code easier to modify and rerun |

---

# 🧪 Practice

Try creating your own variables:

```python
height = 1.79
weight = 68.7

bmi = weight / height ** 2

print(bmi)
print(type(bmi))
```

🚀 **Practice creating variables, checking their types, and experimenting with different data types!**
