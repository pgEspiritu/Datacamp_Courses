# 🔄 `while` Loop in Python

## 📌 Overview

In the previous chapter, you learned about conditional statements such as:

- `if`
- `elif`
- `else`

These statements allow Python to change the flow of a program based on conditions.

A `while` loop is similar to an `if` statement because it also checks a condition.

The key difference is:

- `if` → checks the condition **once**
- `while` → keeps checking the condition and repeatedly executes the code **as long as the condition is `True`**

---

# 🔀 `if` vs `while`

## `if` Statement

An `if` statement executes its code once when the condition is `True`.

    if condition:
        # execute once

After that, Python continues to the next statement.

## `while` Loop

A `while` loop repeatedly executes its code while the condition remains `True`.

    while condition:
        # execute repeatedly

After each iteration, Python goes back to the `while` condition and checks it again.

---

# 🧠 General Syntax

The syntax of a `while` loop is similar to an `if` statement:

    while condition:
        # code to repeat

### Important Rules

- The condition must end with a colon `:`.
- The code inside the loop must be indented.
- The condition is checked before every iteration.
- The loop stops when the condition becomes `False`.

---

# 🔢 Example: Reducing an Error

A `while` loop is useful when you want to **repeat an action until a certain condition is met**.

Suppose a numerical model starts with an error of `50`.

The algorithm reduces the error by dividing it by `4` each time.

We want to keep repeating this process until the error is no longer greater than `1`.

---

## ✅ Code

    error = 50.0

    while error > 1:
        error = error / 4
        print(error)

---

# 🔍 Step-by-Step Execution

The loop condition is:

    error > 1

Initially:

    error = 50.0

So:

    50.0 > 1

is:

    True

The loop executes.

---

## 🔄 First Iteration

The error is divided by `4`:

    50.0 / 4

Result:

    12.5

Output:

    12.5

Python then returns to the `while` condition.

---

## 🔄 Second Iteration

Now:

    error = 12.5

Check:

    12.5 > 1

Result:

    True

The loop executes again:

    12.5 / 4

Result:

    3.125

Output:

    3.125

---

## 🔄 Third Iteration

Now:

    error = 3.125

Check:

    3.125 > 1

Result:

    True

The loop executes again:

    3.125 / 4

Result:

    0.78125

Output:

    0.78125

---

## 🛑 Fourth Condition Check

Now:

    error = 0.78125

Python checks:

    0.78125 > 1

Result:

    False

The code inside the loop is no longer executed.

Python exits the `while` loop and continues with the next statement in the program.

---

# 📊 Execution Summary

| Iteration | Error Before | `error > 1` | Error After |
|---:|---:|---|---:|
| 1 | `50.0` | `True` | `12.5` |
| 2 | `12.5` | `True` | `3.125` |
| 3 | `3.125` | `True` | `0.78125` |
| 4 | `0.78125` | `False` | Loop stops |

The important point is that the value of `error` changes after each iteration.

---

# ⚠️ Avoid Infinite Loops

A `while` loop must eventually reach a point where its condition becomes `False`.

For example:

    error = 50.0

    while error > 1:
        print(error)

This is a problem because `error` is never changed.

The condition:

    error > 1

will always remain:

    True

Therefore, the loop continues forever.

This is called an **infinite loop**.

---

# 🚨 Why Updating the Variable Matters

In a working loop:

    while error > 1:
        error = error / 4

The value of `error` gets smaller every time.

Eventually:

    error <= 1

and the loop stops.

The update inside the loop is therefore **crucial**.

---

# 🛑 Stopping an Infinite Loop

If you accidentally create an infinite loop:

    while True:
        print("This never stops")

you need to interrupt the program manually.

In many Python environments, you can use:

    Ctrl + C

to stop execution.

On DataCamp or similar platforms, an infinite loop may cause the session to be disconnected or interrupted.

---

# 🔄 How a `while` Loop Works

The execution flow is:

    Start
      ↓
    Check condition
      ↓
    Is condition True?
      ↓
    Yes ──→ Execute loop body
      ↑             │
      │             ↓
      └──── Check condition again
                    │
                    ↓
                   No
                    ↓
                 Continue

The loop repeatedly returns to the condition after each iteration.

---

# 🆚 `if` vs `while`

| Feature | `if` | `while` |
|---|---|---|
| Checks condition | Once | Repeatedly |
| Repeats code | No | Yes |
| Runs while condition is `True` | Only once | Until condition becomes `False` |
| Common use | Conditional execution | Repeated execution |

### Example

    if error > 1:
        print(error)

This prints the value at most once.

    while error > 1:
        error = error / 4
        print(error)

This repeatedly updates and prints the value until the condition becomes `False`.

---

# 💡 When to Use a `while` Loop

A `while` loop is useful when you want to:

- Repeat an action until a condition is met.
- Continue processing while a condition remains `True`.
- Perform iterative calculations.
- Gradually reduce or increase a value until it reaches a threshold.
- Repeat a process when the exact number of iterations is not known in advance.

### General Idea

> **"Keep repeating this action while this condition is true."**

---

# 🔑 Key Takeaways

- A `while` loop repeatedly executes code while its condition is `True`.
- The syntax is similar to an `if` statement:

      while condition:
          # code

- Python checks the condition before every iteration.
- The loop stops when the condition becomes `False`.
- The variable controlling the condition should usually be updated inside the loop.
- If the condition never becomes `False`, the program can enter an **infinite loop**.
- `Ctrl + C` can interrupt a running Python program in many environments.

### 📚 Core Pattern

    variable = starting_value

    while condition:
        # update variable
        # perform action

> 💡 **Remember:** A good `while` loop needs a clear condition, a loop body, and a mechanism that eventually makes the condition `False`.
