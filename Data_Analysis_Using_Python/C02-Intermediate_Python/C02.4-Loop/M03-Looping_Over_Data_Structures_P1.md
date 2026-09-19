# 🔁 Looping Over Data Structures — Part 1

## 📌 Overview

You already learned how to use `for` loops with:

- Lists
- Strings

Python also lets you loop over other data structures, such as:

- Dictionaries
- NumPy arrays
- 2D NumPy arrays

The basic `for` loop syntax stays similar, but the way you define the **sequence** depends on the data structure.

---

# 🗺️ Looping Over Dictionaries

Suppose we have a dictionary called `world` containing country names as keys and populations as values:

    world = {
        "afghanistan": 30.55,
        "albania": 2.77,
        "algeria": 39.21
    }

Each dictionary entry is a:

    key : value

pair.

---

# ❌ Why the Basic Approach Does Not Work

You might try:

    for key, value in world:
        print(key, value)

This produces an error.

The reason is that iterating directly over a dictionary gives you its **keys**, not separate key-value pairs.

Python therefore cannot automatically assign two variables:

    key
    value

from a single dictionary key.

---

# ✅ Using `.items()`

To iterate over both the key and value, use the dictionary's `.items()` method:

    for key, value in world.items():
        print(key, value)

The `.items()` method provides a key-value pair during each iteration.

---

# 🔍 How `.items()` Works

For example:

    world = {
        "afghanistan": 30.55,
        "albania": 2.77,
        "algeria": 39.21
    }

Then:

    world.items()

provides pairs conceptually like:

    ("afghanistan", 30.55)
    ("albania", 2.77)
    ("algeria", 39.21)

The `for` loop unpacks each pair into:

    key
    value

---

# 🧠 Variable Names Are Arbitrary

These variable names:

    key
    value

are not special Python keywords.

You could also write:

    for k, v in world.items():
        print(k, v)

The important rule is the order:

- First variable → key
- Second variable → value

For example:

    for k, v in world.items():

means:

    k = key
    v = value

---

# 📌 Dictionary Iteration

### Keys Only

    for key in world:
        print(key)

### Key-Value Pairs

    for key, value in world.items():
        print(key, value)

### Important

Use:

    .items()

when you need **both keys and values**.

---

# 🔢 NumPy Arrays

NumPy arrays can also be iterated over with a `for` loop.

Suppose we have a BMI array:

    bmi = np.array([21.5, 23.1, 19.8, 25.4])

A basic `for` loop works:

    for value in bmi:
        print(value)

Each iteration gives one element from the array.

### Output

    21.5
    23.1
    19.8
    25.4

For a **1D NumPy array**, the basic `for` loop is enough.

---

# 🧮 2D NumPy Arrays

Now consider a 2D NumPy array called `meas`.

For example:

    meas = np.array([
        [1.73, 65.4],
        [1.68, 59.2],
        [1.71, 63.6],
        [1.89, 88.4]
    ])

A basic loop:

    for value in meas:
        print(value)

does **not** print every individual number.

Instead, it prints one entire 1D array at a time:

    [ 1.73 65.4 ]
    [ 1.68 59.2 ]
    [ 1.71 63.6 ]
    [ 1.89 88.4 ]

---

# 🧠 Why Does This Happen?

A 2D NumPy array can be thought of as an **array of 1D arrays**.

For:

    meas = np.array([
        [1.73, 65.4],
        [1.68, 59.2],
        [1.71, 63.6],
        [1.89, 88.4]
    ])

each row is itself a 1D array.

Therefore:

    for value in meas:

iterates over the rows rather than over every individual element.

---

# ✅ Using `np.nditer()`

To iterate over **every individual element** of a NumPy array, use:

    np.nditer()

Example:

    for value in np.nditer(meas):
        print(value)

Now each number is processed separately.

### Output

    1.73
    65.4
    1.68
    59.2
    1.71
    63.6
    1.89
    88.4

---

# 🔍 `np.nditer()`

The function:

    np.nditer(array)

creates an iterator that goes through all elements of the array.

Example:

    for value in np.nditer(meas):
        print(value)

This works even when `meas` is multidimensional.

---

# 🆚 Dictionary vs NumPy Array

Different data structures require different approaches.

| Data Structure | Recommended Approach |
|---|---|
| List | `for value in my_list:` |
| String | `for character in my_string:` |
| Dictionary keys | `for key in my_dict:` |
| Dictionary key-value pairs | `for key, value in my_dict.items():` |
| 1D NumPy array | `for value in array:` |
| 2D NumPy array — every element | `for value in np.nditer(array):` |

---

# 🧠 Important Distinction

### Dictionary

Uses a **method**:

    world.items()

### NumPy Array

Uses a **function**:

    np.nditer(meas)

This is an important distinction to remember.

---

# 📚 Examples

## Dictionary

    world = {
        "afghanistan": 30.55,
        "albania": 2.77,
        "algeria": 39.21
    }

    for country, population in world.items():
        print(country, population)

---

## 1D NumPy Array

    bmi = np.array([21.5, 23.1, 19.8, 25.4])

    for value in bmi:
        print(value)

---

## 2D NumPy Array

    meas = np.array([
        [1.73, 65.4],
        [1.68, 59.2],
        [1.71, 63.6],
        [1.89, 88.4]
    ])

    for value in np.nditer(meas):
        print(value)

---

# 🔑 Key Takeaways

- A basic `for` loop works directly with lists, strings, and 1D NumPy arrays.
- To iterate over **dictionary key-value pairs**, use:

      dictionary.items()

- In:

      for key, value in dictionary.items():

  the first variable receives the key and the second receives the value.
- Variable names such as `key`, `value`, `k`, and `v` are arbitrary.
- A basic loop over a 2D NumPy array processes one row at a time.
- To access **every individual element** of a NumPy array, use:

      np.nditer(array)

- Remember:
  - **Dictionary → method:** `.items()`
  - **NumPy array → function:** `np.nditer()`

### 📚 Core Patterns

**Dictionary key-value pairs:**

    for key, value in my_dict.items():
        print(key, value)

**1D NumPy array:**

    for value in my_array:
        print(value)

**Every element of a multidimensional NumPy array:**

    for value in np.nditer(my_array):
        print(value)
