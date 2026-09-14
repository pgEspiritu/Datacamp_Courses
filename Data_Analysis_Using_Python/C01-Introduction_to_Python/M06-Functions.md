# 🧩 Functions

A **function** is a reusable piece of code designed to perform a specific task.

Instead of writing the same code repeatedly, you can **call a function** whenever you need it.

## 📌 What Is a Function?

You have already used Python functions such as:

    type()

The `type()` function returns the data type of a value.

For example:

    type(1.68)

Functions can be thought of as **black boxes**:

    Input → Function → Output

You provide input to the function, the function performs its task, and it returns an output.

## 🧪 Example: `max()`

Python has a built-in function called `max()` that returns the largest value in a collection.

Suppose:

    fam = [1.73, 1.68, 1.89, 1.65]

You can find the tallest height using:

    max(fam)

Output:

    1.89

Instead of writing your own code to search through the list, you can simply use the built-in `max()` function.

### 💡 Why Use Functions?

- ♻️ Reuse code
- ⏱️ Save time
- 🧹 Avoid unnecessary code
- 🎯 Focus on the task instead of implementing everything yourself

## 📦 Storing a Function Result

You can assign the result of a function to a variable.

For example:

    tallest = max(fam)

Now `tallest` is a regular Python variable containing:

    1.89

You can use it in other calculations:

    tallest + 0.05

## 🔢 The `round()` Function

Another useful built-in function is `round()`.

It can be used to round a number to a specified number of decimal places.

### Basic Syntax

    round(number, ndigits)

Where:

- `number` = the value to round
- `ndigits` = number of decimal places to keep

### Example

    round(1.68, 1)

Output:

    1.7

The first argument is `1.68`, and the second argument specifies `1` decimal place.

## 🔢 Calling `round()` With One Argument

The second argument is optional.

You can also write:

    round(1.68)

When `ndigits` is not provided, Python rounds to the nearest integer.

Output:

    2

## 📌 Function Arguments

The values passed to a function are called **arguments**.

For example:

    round(1.68, 1)

The arguments are:

| Argument | Value |
|---|---:|
| `number` | `1.68` |
| `ndigits` | `1` |

Python matches the provided values to the corresponding function arguments.

In this case:

    number = 1.68
    ndigits = 1

The function then performs its operation and returns the result.

## 🔧 Optional Arguments

An argument can be **optional** when the function has a default behavior for it.

For `round()`:

    round(1.68, 1)

and:

    round(1.68)

are both valid.

When `ndigits` is omitted, Python uses its default behavior and rounds to the nearest integer.

## 📖 Using `help()`

Python provides the `help()` function to display documentation about functions.

Example:

    help(round)

This can show information such as:

- What the function does
- Its arguments
- Which arguments are optional
- How the function should be used

## 🔍 Finding the Right Function

You do not need to memorize every Python function.

For common programming tasks, there is often already a built-in function or library function that can help.

A good approach is:

1. Identify what you want to accomplish.
2. Search for an existing Python function that can perform the task.
3. Check its documentation.
4. Use it instead of writing unnecessary code from scratch.

### 💡 General Rule

If you are performing a **standard or common task**, check whether Python already provides a function for it.

## 🎯 Common Functions So Far

| Function | Purpose | Example |
|---|---|---|
| `type()` | Check the data type | `type(1.68)` |
| `max()` | Find the largest value | `max(fam)` |
| `round()` | Round a number | `round(1.68, 1)` |
| `help()` | Display documentation | `help(round)` |

## 🧠 Key Takeaways

- 🧩 A **function** is reusable code designed for a specific task.
- 📥 Functions can receive **arguments** as input.
- 📤 Functions can return an **output**.
- 📦 Function results can be stored in variables.
- 🔢 `max()` returns the largest value.
- 🔄 `round()` rounds numbers.
- ⚙️ Some function arguments are **optional**.
- 📖 `help()` can be used to learn how a function works.
- 🔍 Before writing your own solution for a common task, check whether Python already has a function that can do it.
- 🚀 Learning and using functions makes Python code shorter, clearer, and more reusable.
