# 🔍 Subsetting Lists

After creating a Python list, you need to know how to **access specific elements** or groups of elements.

Python uses **indexing** and **slicing** to access list elements.

---

# 🔢 List Indexing

Each element in a Python list has an **index**.

⚠️ **Python uses zero-based indexing**, meaning the first element has index `0`.

Example:

```python
fam = [1.73, 1.68, 1.71, 1.65, 1.72]
```

| Element | Index |
| ------- | ----: |
| `1.73`  |   `0` |
| `1.68`  |   `1` |
| `1.71`  |   `2` |
| `1.65`  |   `3` |
| `1.72`  |   `4` |

### 🎯 Access an Element

Use the index inside square brackets `[]`:

```python
fam[1]
```

Output:

```text
1.68
```

### 💡 General Syntax

```python
list_name[index]
```

---

# 🔢 Negative Indexing

Python also allows you to count from the **end of a list** using negative indexes.

| Index | Position       |
| ----: | -------------- |
|  `-1` | Last element   |
|  `-2` | Second-to-last |
|  `-3` | Third-to-last  |
|  `-4` | Fourth-to-last |

Example:

```python
fam[-1]
```

➡️ Returns the **last element**.

```python
fam[-2]
```

➡️ Returns the **second-to-last element**.

### 🔄 Positive vs. Negative Index

The last element can be accessed using either:

```python
fam[4]
```

or:

```python
fam[-1]
```

Both return the same element.

---

# ✂️ List Slicing

**Slicing** allows you to select **multiple elements** from a list and create a new list.

Use a colon `:`.

### 💡 Syntax

```python
list_name[start:end]
```

⚠️ The **start index is included**, but the **end index is excluded**.

Example:

```python
fam[1:4]
```

This selects:

```text
index 1 → included
index 2 → included
index 3 → included
index 4 → excluded
```

Result:

```text
[1.68, 1.71, 1.65]
```

---

# 🎯 Start and End Index

### ✅ Start Included

```python
fam[1:4]
```

Includes index `1`.

### ❌ End Excluded

```python
fam[1:4]
```

Does **not** include index `4`.

> 🧠 **Remember: Start is included, end is excluded.**

---

# ✂️ Omitting the Start Index

You can leave the start index empty.

```python
fam[:3]
```

Python starts from index `0`.

Equivalent to:

```python
fam[0:3]
```

---

# ✂️ Omitting the End Index

You can leave the end index empty.

```python
fam[2:]
```

Python includes everything from index `2` through the end of the list.

---

# 📊 Indexing vs. Slicing

| Operation            | Syntax     | Result                 |
| -------------------- | ---------- | ---------------------- |
| 🔍 Single element    | `fam[3]`   | One value              |
| ✂️ Multiple elements | `fam[1:4]` | New list               |
| ⬅️ From beginning    | `fam[:3]`  | Index `0` through `2`  |
| ➡️ To the end        | `fam[2:]`  | Index `2` through last |
| 🔙 Last element      | `fam[-1]`  | Last value             |

---

# 🧠 Key Takeaways

* 🔢 Python lists use **zero-based indexing**.
* `0` → first element.
* `1` → second element.
* `-1` → last element.
* 🔍 Use `list[index]` to access a single element.
* ✂️ Use `list[start:end]` to select multiple elements.
* ✅ The **start index is included**.
* ❌ The **end index is excluded**.
* ⬅️ Omitting the start means Python starts at `0`.
* ➡️ Omitting the end means Python goes to the end.

### 🚀 Quick Reference

```python
# First element
fam[0]

# Fourth element
fam[3]

# Last element
fam[-1]

# Elements from index 1 to 3
fam[1:4]

# First three elements
fam[:3]

# From index 2 to the end
fam[2:]
```

> 💡 **Master indexing and slicing — they are essential skills for working with lists and data in Python.** 🐍📊
