# 🔀 `if`, `elif`, `else` — Conditional Statements in Python

## 📌 Overview

You now know how to:

- Compare values using operators such as `<`, `>`, `<=`, and `>=`
- Combine Boolean expressions using `and`, `or`, and `not`

The next step is using these results to **control how a Python program behaves**.

Python provides three conditional statements:

- `if`
- `elif`
- `else`

These allow your program to execute different blocks of code depending on whether a condition is `True` or `False`.

---

# 1. `if` Statement

An `if` statement executes a block of code **only when its condition is `True`**.

## 🧠 General Structure

    if condition:
        expression

### Important Rules

- The condition must be followed by a **colon `:`**.
- The code inside the `if` block must be **indented**.
- Four spaces are commonly used for indentation.
- A tab can also be used, but spaces are generally recommended.
- Code without indentation is outside the `if` block.

---

## 🔢 Example: Checking if a Number is Even

Suppose:

    z = 4

To check whether `z` is even:

    if z % 2 == 0:
        print("z is even")

### How It Works

The modulo operator `%` returns the remainder after division.

For an even number:

    4 % 2

Result:

    0

Therefore:

    z % 2 == 0

evaluates to:

    True

So Python executes:

    print("z is even")

### Output

    z is even

---

# 2. Indentation in `if` Statements

Indentation tells Python which statements belong to the `if` block.

Example:

    if z % 2 == 0:
        print("z is even")
        print("The number is divisible by 2.")

Both `print()` statements are indented, so both belong to the `if` statement.

### Output

    z is even
    The number is divisible by 2.

---

## 🚪 Exiting an `if` Statement

To tell Python that the `if` block has ended, continue with code **without indentation**.

Example:

    if z % 2 == 0:
        print("z is even")

    print("This is outside the if statement.")

The second `print()` always executes because it is not part of the `if` block.

---

# 3. What Happens When the Condition is False?

Consider:

    z = 5

    if z % 2 == 0:
        print("z is even")

Since:

    5 % 2

equals:

    1

the condition:

    z % 2 == 0

is `False`.

Therefore, the code inside the `if` block is **not executed**.

### Output

    # No output

---

# 4. `else` Statement

What if you want your program to do something when the `if` condition is `False`?

Use `else`.

## 🧠 General Structure

    if condition:
        expression_if_true
    else:
        expression_if_false

The `else` block does not need its own condition.

It runs whenever the associated `if` condition is `False`.

---

## 🔢 Example: Even or Odd

    z = 5

    if z % 2 == 0:
        print("z is even")
    else:
        print("z is odd")

Since `5` is not divisible by `2`, the `if` condition is `False`.

Python therefore executes the `else` block.

### Output

    z is odd

---

# 5. `elif` Statement

Sometimes you need more than two possible outcomes.

Python provides `elif`, which means **"else if"**.

It allows you to test another condition when the previous condition was `False`.

## 🧠 General Structure

    if condition1:
        expression1
    elif condition2:
        expression2
    else:
        expression3

You can have multiple `elif` statements in a conditional structure.

---

# 🔢 Example: Divisible by 2 or 3

Suppose you want different messages depending on whether a number is divisible by `2` or `3`.

    z = 3

    if z % 2 == 0:
        print("z is divisible by 2")
    elif z % 3 == 0:
        print("z is divisible by 3")

### Step-by-Step

For:

    z = 3

The first condition is:

    z % 2 == 0

which is:

    3 % 2 == 0

Result:

    False

Python then checks the `elif` condition:

    z % 3 == 0

which is:

    3 % 3 == 0

Result:

    True

Therefore Python executes:

    print("z is divisible by 3")

### Output

    z is divisible by 3

---

# 6. Only the First True Condition Executes

This is an important behavior of `if` / `elif` / `else`.

Suppose:

    z = 6

Then both conditions are true:

    z % 2 == 0
    z % 3 == 0

However, Python does **not** execute both blocks.

Example:

    if z % 2 == 0:
        print("z is divisible by 2")
    elif z % 3 == 0:
        print("z is divisible by 3")

The first condition is already `True`, so Python executes its block and then **leaves the conditional structure**.

### Output

    z is divisible by 2

The `elif` condition is never evaluated after the first `True` condition is found.

---

# 🔄 Conditional Flow

Python checks conditions from **top to bottom**:

    if condition1:
        ...
    elif condition2:
        ...
    elif condition3:
        ...
    else:
        ...

The process is:

1. Check the `if` condition.
2. If it is `True`, execute its block and stop.
3. Otherwise, check the first `elif`.
4. Continue checking `elif` conditions until one is `True`.
5. If none are `True`, execute `else` if it exists.

---

# 🧠 `if` vs `elif` vs `else`

| Statement | Purpose |
|---|---|
| `if` | Tests the first condition |
| `elif` | Tests another condition if previous conditions were `False` |
| `else` | Runs when none of the previous conditions are `True` |

---

# 📌 Important Syntax Rules

### ✅ Correct

    if x > 10:
        print("Greater than 10")

### ❌ Missing colon

    if x > 10
        print("Greater than 10")

### ❌ Incorrect indentation

    if x > 10:
    print("Greater than 10")

### ✅ Correct indentation

    if x > 10:
        print("Greater than 10")

---

# 🧪 Example: Complete Conditional Structure

    z = 6

    if z % 2 == 0:
        print("z is divisible by 2")
    elif z % 3 == 0:
        print("z is divisible by 3")
    else:
        print("z is neither divisible by 2 nor 3")

Because `z = 6` satisfies the first condition, the output is:

    z is divisible by 2

Even though `6` is also divisible by `3`, the `elif` block is skipped because the `if` condition was already `True`.

---

# 🔑 Key Takeaways

- `if` executes code when a condition is `True`.
- `elif` allows you to test additional conditions.
- `else` executes when all previous conditions are `False`.
- A colon `:` is required after `if`, `elif`, and `else`.
- Code inside a conditional block must be **indented**.
- Multiple statements can belong to the same conditional block.
- Python evaluates an `if` / `elif` / `else` structure from **top to bottom**.
- Once Python finds a `True` condition, it executes that block and skips the remaining `elif` and `else` blocks.
- `elif` is useful when you need multiple possible conditions.
- `else` does not require a condition.

### 📚 Basic Pattern

    if condition1:
        # code if condition1 is True
    elif condition2:
        # code if condition2 is True
    else:
        # code if all conditions are False
