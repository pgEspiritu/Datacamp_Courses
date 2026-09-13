# 📋 Python Lists

A **Python list** is a data structure used to store a **collection of values** under a single variable name.

---

# 🔢 Python Data Types

Python has several common data types:

| Data Type  | Description          | Example          |
| ---------- | -------------------- | ---------------- |
| 🔢 `int`   | Integer/whole number | `25`             |
| 🔢 `float` | Decimal number       | `1.79`           |
| 🔤 `str`   | Text                 | `"Python"`       |
| ✅ `bool`   | Logical value        | `True` / `False` |
| 📋 `list`  | Collection of values | `[1, 2, 3]`      |

A variable normally represents a single value:

```python id="8h9e2v"
height = 1.79
```

But when you need to store **multiple values**, a list is more convenient.

---

# 📋 Creating a List

Lists are created using **square brackets `[]`**.

Example:

```python id="b6q9dm"
fam = [1.73, 1.68, 1.79, 1.65]
```

The list can then be accessed using its variable name:

```python id="7f3f2q"
print(fam)
```

Output:

```text id="j0w3k5"
[1.73, 1.68, 1.79, 1.65]
```

### 💡 Important

A list gives a **single name to a collection of values**.

Instead of creating separate variables:

```python id="h4gk7m"
height1 = 1.73
height2 = 1.68
height3 = 1.79
height4 = 1.65
```

You can use one list:

```python id="2n6qz9"
heights = [1.73, 1.68, 1.79, 1.65]
```

---

# 🧩 List Elements

The individual values inside a list are called **elements**.

Example:

```python id="5v8y1q"
fam = [1.73, 1.68, 1.79, 1.65]
```

The elements are:

```text
1.73
1.68
1.79
1.65
```

A list can contain different Python data types:

```python id="4z0w3x"
my_list = [1, 3.14, "Python", True]
```

So a list can contain:

* 🔢 Integers
* 🔢 Floats
* 🔤 Strings
* ✅ Booleans
* 📋 Other lists

---

# 📋 Lists of Lists

Python lists can contain **other lists**.

These are sometimes called **nested lists**.

Example:

```python id="7x2m9a"
fam2 = [
    ["Liz", 1.73],
    ["Emma", 1.68],
    ["Dad", 1.79],
    ["Mom", 1.65]
]
```

Here:

* `fam2` is the main list.
* Each inner list represents one family member.
* The main list contains **four sublists**.

You can also think of it as:

```text
fam2
├── ["Liz", 1.73]
├── ["Emma", 1.68]
├── ["Dad", 1.79]
└── ["Mom", 1.65]
```

---

# 🔍 Checking the List Type

Use `type()` to check whether a variable is a list:

```python id="j5s8qc"
type(fam)
```

Output:

```text
<class 'list'>
```

You can also check a nested list:

```python id="z4p7ks"
type(fam2)
```

Output:

```text
<class 'list'>
```

---

# 🧠 Key Takeaways

* 📋 A **list** stores multiple values under one variable name.
* `[]` are used to create lists.
* 🧩 Individual values in a list are called **elements**.
* 🔢 Lists can contain different data types.
* 📋 Lists can contain **other lists**.
* 🪆 A list containing other lists is called a **nested list**.
* 🔍 Use `type()` to check whether a variable is a list.

### 💡 Basic Syntax

```python id="4a2c7v"
my_list = [value1, value2, value3]
```

Example:

```python id="8d5n1m"
heights = [1.73, 1.68, 1.79, 1.65]
```

### 🪆 Nested List Syntax

```python id="6p2k8r"
my_list = [
    [value1, value2],
    [value3, value4]
]
```

🚀 **Lists are one of the most important Python data structures for working with collections of data.**
