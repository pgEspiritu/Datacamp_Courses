# 🔁 `for` Loop in Python

## 📌 Overview

Python has another type of loop besides the `while` loop: the **`for` loop**.

A `for` loop is useful when you want to repeat an action for **each item in a sequence**, such as:

- Lists
- Strings
- Tuples
- Other iterable objects

The basic idea is:

> **For each item in a sequence, execute some code.**

---

# 🧠 Basic `for` Loop Syntax

The general recipe is:

    for variable in sequence:
        # code to execute

This can be read as:

> For each `variable` in `sequence`, execute the code.

### Example

    for height in fam:
        print(height)

Here:

- `height` → variable that stores the current item
- `fam` → sequence being iterated over
- `print(height)` → code executed for every item

---

# 👨‍👩‍👧‍👦 Example: Loop Through a List

Suppose `fam` contains the heights of your family:

    fam = [1.73, 1.68, 1.71, 1.89]

Without a `for` loop, you could print every element separately:

    print(fam[0])
    print(fam[1])
    print(fam[2])
    print(fam[3])

This works, but it is repetitive.

A `for` loop is much cleaner:

    for height in fam:
        print(height)

### Output

    1.73
    1.68
    1.71
    1.89

---

# 🔄 How a `for` Loop Works

When Python encounters:

    for height in fam:
        print(height)

it first looks at the sequence:

    fam = [1.73, 1.68, 1.71, 1.89]

Python then goes through each element one at a time.

### First Iteration

Python stores:

    1.73

in:

    height

Then executes:

    print(height)

Output:

    1.73

### Second Iteration

Python stores:

    1.68

in:

    height

Output:

    1.68

### Third Iteration

Python stores:

    1.71

in:

    height

Output:

    1.71

### Fourth Iteration

Python stores:

    1.89

in:

    height

Output:

    1.89

After all elements have been processed, the loop ends.

---

# 💡 The Loop Variable is Arbitrary

The variable name used in a `for` loop is up to you.

These all work:

    for height in fam:
        print(height)

    for h in fam:
        print(h)

    for value in fam:
        print(value)

The important part is that the variable represents the **current item** during each iteration.

---

# 🔢 Accessing the Index with `enumerate()`

A basic `for` loop gives you the values, but it does not automatically give you their indexes.

For example:

    for height in fam:
        print(height)

You have access to:

    height

but not directly to:

    0, 1, 2, 3

If you also want the index, use:

    enumerate()

---

# 🧠 `enumerate()`

The `enumerate()` function produces **two values** for every iteration:

1. The index
2. The corresponding value

### Syntax

    for index, value in enumerate(sequence):
        # code

For the `fam` list:

    for index, height in enumerate(fam):
        print(index, height)

Python produces pairs like:

    (0, 1.73)
    (1, 1.68)
    (2, 1.71)
    (3, 1.89)

---

# 🔢 Example with `enumerate()`

    fam = [1.73, 1.68, 1.71, 1.89]

    for index, height in enumerate(fam):
        print(index, height)

### Output

    0 1.73
    1 1.68
    2 1.71
    3 1.89

Now you have access to both:

    index

and:

    height

---

# 🧩 Using `str()` with `enumerate()`

If you want to build a single string from numbers and text, convert the numbers to strings first.

Example:

    for index, height in enumerate(fam):
        print("index " + str(index) + ": " + str(height))

### Output

    index 0: 1.73
    index 1: 1.68
    index 2: 1.71
    index 3: 1.89

### Why `str()`?

`index` and `height` are numeric values.

Python cannot directly concatenate a number with a string using `+`.

For example, this causes a type error:

    "index " + index

Instead, convert the number:

    "index " + str(index)

---

# 🔤 Looping Over a String

A `for` loop does not only work with lists.

You can also iterate over the characters of a string.

Example:

    for c in "family":
        print(c)

Python processes each character individually.

### Output

    f
    a
    m
    i
    l
    y

Each iteration stores one character in `c`.

---

# 🔠 Example: Capitalize Each Character

You can call string methods inside the loop.

    for c in "family":
        print(c.capitalize())

### Output

    F
    A
    M
    I
    L
    Y

The `.capitalize()` method converts the character to its capitalized form.

---

# 🆚 `for` vs `while`

| Feature | `for` | `while` |
|---|---|---|
| Main purpose | Iterate over a sequence | Repeat while a condition is `True` |
| Typical use | Process every item | Continue until a condition changes |
| Number of iterations | Usually determined by sequence | Determined by condition |
| Example | `for x in values:` | `while x > 0:` |

### `for` Example

    for height in fam:
        print(height)

This processes every element in `fam`.

### `while` Example

    while error > 1:
        error = error / 4

This continues until `error > 1` becomes `False`.

---

# 🧠 Important Concepts

## Iteration

**Iteration** means going through items one at a time.

For:

    fam = [1.73, 1.68, 1.71, 1.89]

the loop iterates over:

    1.73
    1.68
    1.71
    1.89

---

## Iterable

An object that can be iterated over is called an **iterable**.

Examples include:

    [1, 2, 3]

    "family"

    ("a", "b", "c")

Many Python data structures can be used in `for` loops.

---

# ⚠️ Indentation

Just like `if` and `while`, the code inside a `for` loop must be indented.

### ✅ Correct

    for height in fam:
        print(height)

### ❌ Incorrect

    for height in fam:
    print(height)

The indentation tells Python which statements belong to the loop.

---

# 🔑 Key Takeaways

- A `for` loop iterates over the items in a sequence.
- The basic syntax is:

      for variable in sequence:
          # code

- The loop variable stores the current item.
- The variable name can be anything meaningful.
- `enumerate()` gives you both the **index** and the **value**:

      for index, value in enumerate(sequence):
          # code

- Strings can also be iterated over character by character.
- Use `str()` when you need to combine numeric values with strings using `+`.
- The code inside a `for` loop must be indented.

### 📚 Core Patterns

#### Loop Through a List

    for item in my_list:
        print(item)

#### Loop Through a List with Index

    for index, item in enumerate(my_list):
        print(index, item)

#### Loop Through a String

    for character in "Python":
        print(character)

> 💡 **Core idea:** A `for` loop lets you perform the same action for every item in a sequence without writing separate code for each item.
