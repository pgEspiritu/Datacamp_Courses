# 🐍 Python Cheatsheet — Introduction to Python + Intermediate Python

> 📚 Consolidated from the Python lessons, exercises, solutions, and examples you sent.
>
> Covers the core material from **Introduction to Python** and **Intermediate Python**, including Python basics, lists, functions, packages, NumPy, Matplotlib, dictionaries, Pandas, Boolean logic, control flow, loops, DataFrame iteration, random numbers, random walks, simulations, and distributions.

---

# 📘 PART 1 — INTRODUCTION TO PYTHON

# 1. 🐍 Python Basics

## Hello Python

Python is a general-purpose programming language commonly used for:

- Data analysis
- Automation
- Web development
- Machine learning
- Scientific computing
- Scripting

### Basic Python statement

    print("Hello World!")

### Comments

Use `#` for comments:

    # This is a comment
    print("Hello")

---

# 2. 📦 Variables and Types

A variable stores a value.

    x = 5
    name = "Gio"
    height = 1.75

## Common Python Data Types

| Type | Example | Meaning |
|---|---|---|
| `int` | `5` | Integer |
| `float` | `5.5` | Decimal number |
| `str` | `"Python"` | String/text |
| `bool` | `True` | Boolean |
| `list` | `[1, 2, 3]` | Ordered collection |
| `dict` | `{"a": 1}` | Key-value collection |

Check a type using:

    type(x)

Example:

    type(5)

Output:

    <class 'int'>

---

# 3. ✏️ Variable Assignment

Assignment uses:

    =

Example:

    x = 10

This means:

> Store the value `10` in variable `x`.

Do not confuse:

    =

with:

    ==

| Operator | Purpose |
|---|---|
| `=` | Assignment |
| `==` | Equality comparison |

Example:

    x = 10

    x == 10

---

# 4. ➕ Calculations with Variables

Python supports standard arithmetic operators.

| Operator | Meaning | Example |
|---|---|---|
| `+` | Addition | `5 + 2` |
| `-` | Subtraction | `5 - 2` |
| `*` | Multiplication | `5 * 2` |
| `/` | Division | `5 / 2` |
| `//` | Floor division | `5 // 2` |
| `%` | Modulo/remainder | `5 % 2` |
| `**` | Exponentiation | `5 ** 2` |

Examples:

    x = 5
    y = 2

    x + y
    x - y
    x * y
    x / y
    x // y
    x % y
    x ** y

### Modulo

Useful for checking even/odd values:

    4 % 2 == 0

`True` → even

    5 % 2 == 0

`False` → odd

---

# 5. 🔤 Strings

Strings are text enclosed in quotes.

    "Python"
    'Python'

### String Concatenation

Use `+`:

    "Hello " + "World"

Output:

    Hello World

### String Repetition

    "Hi " * 3

Output:

    Hi Hi Hi

### String Length

    len("Python")

Output:

    6

### String Conversion

Convert numbers to strings with:

    str(123)

Convert strings to numbers:

    int("123")
    float("3.14")

---

# 6. 🔄 Other Basic Types

## Boolean

Only two Boolean values exist:

    True
    False

Python is case-sensitive:

    True     # correct
    true     # not the Boolean value

## Integer

    x = 10

## Float

    x = 10.5

## String

    x = "hello"

---

# 7. 📋 Python Lists

A list stores multiple values in an ordered collection.

    areas = [11.25, 18.0, 20.0, 10.75, 9.50]

Lists can contain different types:

    mixed = [1, 2.5, "Python", True]

---

# 8. 🏠 List of Lists

A list can contain other lists.

    house = [
        ["hallway", 11.25],
        ["kitchen", 18.0],
        ["living room", 20.0],
        ["bedroom", 10.75],
        ["bathroom", 9.50]
    ]

Each sublist contains:

    [room_name, area]

---

# 9. 🔢 List Indexing

Python uses **zero-based indexing**.

    areas = [11.25, 18.0, 20.0, 10.75, 9.50]

Indexes:

    0 → 11.25
    1 → 18.0
    2 → 20.0
    3 → 10.75
    4 → 9.50

Access an element:

    areas[0]

Output:

    11.25

---

# 10. 🔙 Negative Indexing

Negative indexes count from the end.

    areas[-1]

Returns the last value.

    areas[-2]

Returns the second-to-last value.

Important:

    list[-1]

is a common way to access the **last element**.

---

# 11. ✂️ List Slicing

Syntax:

    list[start:end]

Important:

> Start is included, end is excluded.

Example:

    areas[1:4]

selects indexes:

    1, 2, 3

### Examples

    areas[:3]

First three elements.

    areas[2:]

Everything from index `2` onward.

    areas[:]

Entire list.

    areas[-3:]

Last three elements.

---

# 12. 🏠 Subsetting a List of Lists

Example:

    house = [
        ["hallway", 11.25],
        ["kitchen", 18.0],
        ["living room", 20.0],
        ["bedroom", 10.75],
        ["bathroom", 9.50]
    ]

Get the first room:

    house[0]

Get the room name:

    house[0][0]

Get the room area:

    house[0][1]

Get the last room's area:

    house[-1][1]

---

# 13. ✏️ Changing List Elements

Lists are mutable.

    areas[0] = 12.0

Changes the first value.

---

# 14. ➕ Adding Elements to Lists

## `append()`

Adds one item to the end.

    areas.append(15.0)

## `extend()`

Adds multiple items.

    areas.extend([12.0, 13.0])

Example:

    x = [1, 2]

    x.extend([3, 4])

Result:

    [1, 2, 3, 4]

---

# 15. ➖ Removing Elements

## `del`

Remove by index:

    del areas[0]

## `pop()`

Remove and return an element:

    areas.pop()

Remove a specific index:

    areas.pop(0)

---

# 16. 🧠 Lists Store References

A list variable refers to a list object.

Example:

    x = [1, 2, 3]
    y = x

Now both refer to the same list.

Changing:

    y[0] = 100

also changes:

    x

To create an independent copy:

    y = x.copy()

---

# 17. 🛠️ Functions

A function is reusable code.

Examples of built-in functions:

    print()
    len()
    type()
    max()
    min()
    sum()
    sorted()
    round()

---

# 18. 🔢 Useful Built-in Functions

## `len()`

    len([1, 2, 3])

Returns:

    3

## `max()`

    max([3, 7, 2])

Returns:

    7

## `min()`

    min([3, 7, 2])

Returns:

    2

## `sum()`

    sum([1, 2, 3])

Returns:

    6

## `sorted()`

    sorted([3, 1, 2])

Returns:

    [1, 2, 3]

Descending:

    sorted([3, 1, 2], reverse=True)

Returns:

    [3, 2, 1]

## `round()`

    round(3.14159, 2)

Returns:

    3.14

---

# 19. 🎯 Functions with Multiple Arguments

Some functions accept multiple arguments.

Example:

    round(3.14159, 2)

Arguments:

    number = 3.14159
    ndigits = 2

Another example:

    sorted(values, reverse=True)

---

# 20. 🧰 Methods

Methods are functions associated with an object.

Examples:

    my_list.append(10)

    my_string.upper()

    my_string.lower()

    my_string.capitalize()

    my_string.replace("a", "b")

---

# 21. 🔤 Common String Methods

| Method | Purpose |
|---|---|
| `.upper()` | Uppercase |
| `.lower()` | Lowercase |
| `.capitalize()` | Capitalize first character |
| `.replace()` | Replace text |
| `.strip()` | Remove surrounding whitespace |
| `.split()` | Split a string |
| `.find()` | Find position |
| `.startswith()` | Check beginning |
| `.endswith()` | Check ending |

Examples:

    "python".upper()

    "PYTHON".lower()

    "python".capitalize()

    "Python Python".replace("Python", "Java")

---

# 22. 📋 Common List Methods

| Method | Purpose |
|---|---|
| `.append()` | Add one item |
| `.extend()` | Add multiple items |
| `.pop()` | Remove/return item |
| `.remove()` | Remove matching item |
| `.reverse()` | Reverse in place |
| `.sort()` | Sort in place |
| `.index()` | Find index |
| `.count()` | Count occurrences |

---

# 23. 📦 Packages

A package contains reusable Python functionality.

Import a package:

    import numpy

Use it:

    numpy.array([1, 2, 3])

---

# 24. 🧩 Aliases

Use `as` to give an import a shorter name.

    import numpy as np

Now:

    np.array([1, 2, 3])

A standard convention is:

    import numpy as np

---

# 25. 🎯 Selective Import

Import a specific function:

    from math import pi

Import multiple items:

    from math import pi, sqrt

Then:

    sqrt(16)

instead of:

    math.sqrt(16)

---

# 26. 🔢 NumPy Basics

NumPy is heavily used for numerical computing.

Import:

    import numpy as np

Create an array:

    np.array([1, 2, 3])

---

# 27. 🧮 NumPy Arrays

Example:

    np_height = np.array([74, 70, 72, 75])

NumPy arrays are designed for efficient numerical operations.

---

# 28. ⚡ NumPy Element-Wise Operations

Given:

    x = np.array([1, 2, 3])

You can do:

    x + 10

Result:

    [11 12 13]

Multiplication:

    x * 2

Result:

    [2 4 6]

Exponentiation:

    x ** 2

Result:

    [1 4 9]

---

# 29. 🏀 NumPy Baseball Data

Typical example arrays:

    np_height = np.array([...])

A 2D array may contain height and weight:

    np_baseball = np.array([
        [74, 180],
        [70, 160],
        [72, 190]
    ])

---

# 30. 🔢 2D NumPy Arrays

A 2D array has rows and columns.

    array = np.array([
        [1, 2],
        [3, 4],
        [5, 6]
    ])

Shape:

    array.shape

Returns:

    (3, 2)

Meaning:

- 3 rows
- 2 columns

---

# 31. 🔍 NumPy Subsetting

1D:

    x[0]

2D:

    x[0, 1]

Select row:

    x[0, :]

Select column:

    x[:, 1]

---

# 32. ⚖️ NumPy Statistics

Common functions:

    np.mean(data)
    np.median(data)
    np.std(data)
    np.sum(data)
    np.min(data)
    np.max(data)

### Mean vs Median

Mean:

    np.mean(data)

Median:

    np.median(data)

Median is less affected by extreme outliers.

---

# 33. 📊 Boolean Filtering with NumPy

Comparison:

    bmi > 21

produces a Boolean array.

Example:

    bmi = np.array([20.5, 21.3, 22.4, 24.1])

    bmi > 21

Result:

    [False  True  True  True]

Use it to filter:

    bmi[bmi > 21]

---

# 34. 📈 Matplotlib Basics

Import:

    import matplotlib.pyplot as plt

---

# 35. 📉 Line Plot

    plt.plot(x, y)
    plt.show()

If only one list is provided:

    plt.plot(values)

Python uses:

- index → x-axis
- values → y-axis

---

# 36. 📍 Scatter Plot

    plt.scatter(x, y)
    plt.show()

Useful for showing the relationship between two numerical variables.

---

# 37. 📊 Histogram

    plt.hist(values)
    plt.show()

Specify bins:

    plt.hist(values, bins=10)
    plt.show()

Histograms visualize the distribution of numerical values.

---

# 38. 🎨 Matplotlib Customization

## Labels

    plt.xlabel("X label")
    plt.ylabel("Y label")

## Title

    plt.title("My Plot")

## Ticks

    plt.xticks([0, 1, 2])

## Grid

    plt.grid(True)

## Text

    plt.text(x, y, "Label")

## Size

Scatter:

    plt.scatter(x, y, s=100)

Histogram:

    plt.hist(values, bins=10)

## Color

    plt.scatter(x, y, c="red")

## Transparency

    plt.scatter(x, y, alpha=0.5)

---

# 39. 📖 Dictionaries

A dictionary stores **key-value pairs**.

    europe = {
        "spain": "madrid",
        "france": "paris",
        "germany": "berlin"
    }

Structure:

    key : value

---

# 40. 🔑 Access Dictionary Values

    europe["spain"]

Returns:

    "madrid"

---

# 41. ✏️ Modify Dictionaries

Add:

    europe["italy"] = "rome"

Change:

    europe["france"] = "paris"

Delete:

    del europe["france"]

---

# 42. 🔍 Dictionary Methods

## Keys

    europe.keys()

## Values

    europe.values()

## Key-value pairs

    europe.items()

---

# 43. 🪆 Dictionary of Dictionaries

Dictionaries can contain dictionaries.

Example:

    world = {
        "europe": {
            "spain": "madrid",
            "france": "paris"
        },
        "asia": {
            "japan": "tokyo"
        }
    }

This is often called **dictionary nesting** or "dictionariception".

---

# 44. 🐼 Pandas

Pandas is a major Python library for data manipulation and analysis.

Import:

    import pandas as pd

---

# 45. 📊 DataFrame

A DataFrame is a table-like data structure.

It contains:

- Rows → observations
- Columns → variables/features
- Index → row labels

Example:

    data = {
        "country": ["Brazil", "Russia"],
        "area": [8.5, 17.1]
    }

    df = pd.DataFrame(data)

---

# 46. 🏗️ Dictionary to DataFrame

    data = {
        "country": ["Brazil", "Russia"],
        "area": [8.5, 17.1]
    }

    df = pd.DataFrame(data)

---

# 47. 🔢 DataFrame Index

Access the index:

    df.index

Access columns:

    df.columns

---

# 48. 📥 Read CSV

    cars = pd.read_csv("cars.csv")

Use the first CSV column as index:

    cars = pd.read_csv("cars.csv", index_col=0)

---

# 49. 📊 Series vs DataFrame

Single brackets:

    cars["country"]

returns a **Series**.

Double brackets:

    cars[["country"]]

returns a **DataFrame**.

Multiple columns:

    cars[["country", "cars_per_cap"]]

---

# 50. 🏷️ `loc[]`

`loc[]` is **label-based**.

    cars.loc["US"]

Specific row and column:

    cars.loc["US", "country"]

All rows, one column:

    cars.loc[:, "country"]

---

# 51. 🔢 `iloc[]`

`iloc[]` is **integer-position-based**.

    cars.iloc[0]

First row.

    cars.iloc[0, 1]

First row, second column.

    cars.iloc[:, 1]

All rows, second column.

---

# 52. 🆚 `loc` vs `iloc`

| Method | Uses |
|---|---|
| `loc[]` | Labels |
| `iloc[]` | Integer positions |

Example:

    cars.loc["US", "cars_per_cap"]

versus:

    cars.iloc[0, 1]

---

# 📘 PART 2 — INTERMEDIATE PYTHON

# 53. ⚖️ Comparison Operators

Comparison expressions return:

    True
    False

| Operator | Meaning |
|---|---|
| `==` | Equal |
| `!=` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

---

# 54. Equality

Examples:

    2 == (1 + 1)

    "intermediate" != "python"

    True != False

    "Python" != "python"

Python strings are case-sensitive.

---

# 55. Boolean and Integer Comparisons

Python treats:

    True

like:

    1

and:

    False

like:

    0

Therefore:

    True == 1

returns:

    True

and:

    False == 0

returns:

    True

---

# 56. Greater Than and Less Than

Examples:

    3 < 4
    3 <= 4
    5 > 2
    5 >= 5

Invalid syntax:

    =<
    =>

Correct:

    <=
    >=

---

# 57. String Comparison

Strings are compared lexicographically.

Example:

    "alpha" < "beta"

returns:

    True

String comparisons are case-sensitive.

---

# 58. NumPy Comparison Operators

NumPy performs comparisons element-wise.

    my_house = np.array([18.0, 20.0, 10.75, 9.50])

    my_house >= 18

Result:

    [ True  True False False]

Compare two arrays:

    my_house < your_house

This compares corresponding elements.

---

# 59. 🔘 Boolean Operators

The three basic Boolean operators are:

| Operator | Meaning |
|---|---|
| `and` | Both conditions must be true |
| `or` | At least one condition must be true |
| `not` | Negates the Boolean value |

---

# 60. `and`

Truth table:

| A | B | `A and B` |
|---|---|---|
| `True` | `True` | `True` |
| `True` | `False` | `False` |
| `False` | `True` | `False` |
| `False` | `False` | `False` |

Example:

    x = 12

    x > 5 and x < 15

Result:

    True

---

# 61. `or`

Truth table:

| A | B | `A or B` |
|---|---|---|
| `True` | `True` | `True` |
| `True` | `False` | `True` |
| `False` | `True` | `True` |
| `False` | `False` | `False` |

Example:

    y = 5

    y < 7 or y > 13

Result:

    True

---

# 62. `not`

Reverses a Boolean.

    not True

Returns:

    False

    not False

Returns:

    True

---

# 63. 🧮 NumPy Boolean Functions

Python's:

    and
    or
    not

should not be used to combine NumPy Boolean arrays.

Use:

| Python | NumPy |
|---|---|
| `and` | `np.logical_and()` |
| `or` | `np.logical_or()` |
| `not` | `np.logical_not()` |

---

# 64. `np.logical_and()`

    np.logical_and(condition1, condition2)

Example:

    np.logical_and(my_house > 13, your_house < 15)

Both conditions must be true.

---

# 65. `np.logical_or()`

    np.logical_or(condition1, condition2)

Example:

    np.logical_or(my_house > 18.5, my_house < 10)

At least one condition must be true.

---

# 66. `np.logical_not()`

    np.logical_not(condition)

Reverses Boolean values.

---

# 67. 🔎 Boolean Filtering with NumPy

Example:

    bmi[np.logical_and(bmi > 21, bmi < 22)]

This selects only values:

    > 21

and:

    < 22

---

# 68. 🔀 `if`

Execute code only if a condition is true.

    if condition:
        # code

Example:

    z = 4

    if z % 2 == 0:
        print("z is even")

---

# 69. `else`

Runs when the `if` condition is false.

    if condition:
        # true
    else:
        # false

Example:

    z = 5

    if z % 2 == 0:
        print("z is even")
    else:
        print("z is odd")

---

# 70. `elif`

Used for additional conditions.

    if condition1:
        ...
    elif condition2:
        ...
    else:
        ...

Python checks conditions from top to bottom.

Once one condition is true, the remaining `elif` and `else` blocks are skipped.

---

# 71. ⚠️ `if` / `elif` / `else` Rules

- End the condition with `:`
- Indent the code inside the block.
- Usually use 4 spaces.
- Only the first true branch runs.

Example:

    if area > 15:
        print("big place!")
    elif area > 10:
        print("medium size, nice!")
    else:
        print("pretty small.")

---

# 72. 🏠 Pandas DataFrame Filtering

Boolean filtering uses a Boolean Series.

Example:

    brics["area"] > 8

produces `True`/`False` values.

Use it to filter:

    brics[brics["area"] > 8]

---

# 73. Boolean Filtering — Step by Step

    is_huge = brics["area"] > 8

    brics[is_huge]

Or one line:

    brics[brics["area"] > 8]

---

# 74. Multiple Pandas Conditions

Use NumPy logical functions.

Example:

    import numpy as np

    brics[
        np.logical_and(
            brics["area"] > 8,
            brics["area"] < 10
        )
    ]

This selects values:

    8 < area < 10

---

# 75. 🚗 `cars` Dataset

Typical columns:

| Column | Meaning |
|---|---|
| `country` | Country |
| `cars_per_cap` | Cars per 1,000 people |
| `drives_right` | Whether people drive right |

Example:

    cars = pd.read_csv("cars.csv", index_col=0)

---

# 76. 🚘 Filter Boolean Column

Extract:

    dr = cars["drives_right"]

Then:

    sel = cars[dr]

One-liner:

    sel = cars[cars["drives_right"]]

---

# 77. ✅ `assert`

Check that a condition is true:

    assert sel["drives_right"].all()

`.all()` returns true if every value is true.

---

# 78. 🚗 Cars Per Capita Filtering

Extract:

    cpc = cars["cars_per_cap"]

Create Boolean condition:

    many_cars = cpc > 500

Filter:

    car_maniac = cars[many_cars]

One-liner:

    car_maniac = cars[cars["cars_per_cap"] > 500]

---

# 79. Between Two Values

Example:

    cpc = cars["cars_per_cap"]

    between = np.logical_and(cpc < 500, cpc > 100)

    medium = cars[between]

One-liner:

    medium = cars[
        np.logical_and(
            cars["cars_per_cap"] < 500,
            cars["cars_per_cap"] > 100
        )
    ]

---

# 80. 🔄 `while` Loop

A `while` loop repeats code as long as its condition is true.

Syntax:

    while condition:
        # repeated code

Difference:

- `if` → checks once
- `while` → repeats

---

# 81. `while` Example

    error = 50.0

    while error > 1:
        error = error / 4
        print(error)

Output:

    12.5
    3.125
    0.78125

The loop stops when:

    error > 1

becomes false.

---

# 82. ⚠️ Infinite `while` Loops

Bad example:

    error = 50

    while error > 1:
        print(error)

`error` never changes.

Therefore:

    error > 1

always remains true.

This produces an infinite loop.

---

# 83. 🎯 Correcting Toward Zero

Example:

    offset = -6

    while offset != 0:
        print("correcting...")

        if offset > 0:
            offset = offset - 1
        else:
            offset = offset + 1

        print(offset)

The value moves toward zero:

    -6 → -5 → -4 → -3 → -2 → -1 → 0

---

# 84. ➕ `+=` and `-=`

Instead of:

    x = x + 1

use:

    x += 1

Instead of:

    x = x - 1

use:

    x -= 1

Other examples:

    x *= 2
    x /= 2

---

# 85. 🔁 `for` Loops

A `for` loop iterates over a sequence.

Syntax:

    for variable in sequence:
        # code

Example:

    fam = [1.73, 1.68, 1.71, 1.89]

    for height in fam:
        print(height)

---

# 86. Loop Over a List

    areas = [11.25, 18.0, 20.0, 10.75, 9.50]

    for area in areas:
        print(area)

Output:

    11.25
    18.0
    20.0
    10.75
    9.5

---

# 87. 🔢 `enumerate()`

Use `enumerate()` when you need both:

- Index
- Value

Syntax:

    for index, value in enumerate(sequence):
        # code

Example:

    for index, area in enumerate(areas):
        print(index, area)

---

# 88. Human-Friendly Numbering

Python indexes start at `0`.

For display starting at `1`:

    for index, area in enumerate(areas):
        print("room " + str(index + 1) + ": " + str(area))

Output:

    room 1: 11.25
    room 2: 18.0
    room 3: 20.0
    room 4: 10.75
    room 5: 9.5

---

# 89. 🏠 Loop Over a List of Lists

Given:

    house = [
        ["hallway", 11.25],
        ["kitchen", 18.0],
        ["living room", 20.0],
        ["bedroom", 10.75],
        ["bathroom", 9.50]
    ]

Use unpacking:

    for room, area in house:
        print("the " + room + " is " + str(area) + " sqm")

---

# 90. 🧩 Unpacking

Given:

    room = ["kitchen", 18.0]

You can unpack:

    x, y = room

Now:

    x == "kitchen"
    y == 18.0

The same happens inside:

    for x, y in house:
        ...

---

# 91. 🗺️ Loop Over Dictionaries

To iterate over both keys and values:

    for key, value in dictionary.items():
        print(key, value)

Example:

    europe = {
        "spain": "madrid",
        "france": "paris",
        "germany": "berlin"
    }

    for country, capital in europe.items():
        print("the capital of " + country + " is " + capital)

---

# 92. Dictionary Loop Patterns

Keys:

    for key in europe:
        print(key)

Values:

    for value in europe.values():
        print(value)

Keys + values:

    for key, value in europe.items():
        print(key, value)

---

# 93. 🔢 Loop Over NumPy Arrays

For a 1D array:

    for x in np_height:
        print(x)

For a multidimensional array:

    for x in np.nditer(np_baseball):
        print(x)

---

# 94. `np.nditer()`

A basic loop over a 2D array processes one row at a time.

    for x in np_baseball:
        print(x)

Use:

    for x in np.nditer(np_baseball):
        print(x)

to iterate over every individual element.

---

# 95. 🐼 Loop Over DataFrames

A normal DataFrame loop:

    for x in cars:
        print(x)

iterates over **column names**.

To iterate over rows:

    for lab, row in cars.iterrows():
        print(lab)
        print(row)

---

# 96. `iterrows()`

On every iteration:

- `lab` → row label
- `row` → row as a Pandas Series

Example:

    for lab, row in cars.iterrows():
        print(lab + ": " + str(row["cars_per_cap"]))

Possible output:

    US: 809
    AUS: 731
    JPN: 588

---

# 97. 🔎 Access Data from a Row

Because `row` is a Series:

    row["country"]

    row["cars_per_cap"]

    row["drives_right"]

---

# 98. ➕ Add a DataFrame Column with `iterrows()`

Example:

    for lab, row in cars.iterrows():
        cars.loc[lab, "COUNTRY"] = row["country"].upper()

---

# 99. 🚀 `apply()`

For column transformations, `.apply()` is generally cleaner and more efficient.

Example:

    brics["name_length"] = brics["country"].apply(len)

---

# 100. 🔤 `apply(str.upper)`

Because `upper()` is a string method:

    cars["COUNTRY"] = cars["country"].apply(str.upper)

Alternative Pandas string operation:

    cars["COUNTRY"] = cars["country"].str.upper()

---

# 101. 🆚 `iterrows()` vs `apply()`

## `iterrows()`

    for lab, row in cars.iterrows():
        cars.loc[lab, "COUNTRY"] = row["country"].upper()

Best for:

- Learning row iteration
- Cases where row-wise logic is genuinely needed

## `apply()`

    cars["COUNTRY"] = cars["country"].apply(str.upper)

Better for:

- Applying a function to an entire Series
- Column transformations
- More concise code

---

# 102. 🎲 Random Numbers

NumPy random functions:

    np.random.rand()
    np.random.randint()

---

# 103. 🌱 Random Seed

Set a reproducible random sequence:

    np.random.seed(123)

The same seed produces the same pseudo-random sequence.

Important:

> Same seed + same code → reproducible random sequence.

---

# 104. 🎲 `np.random.rand()`

Generates a random float:

    np.random.rand()

The result is between:

    0 <= value < 1

Example:

    np.random.seed(123)
    print(np.random.rand())

---

# 105. 🔢 `np.random.randint()`

Syntax:

    np.random.randint(low, high)

Important:

> `low` is included, `high` is excluded.

Examples:

    np.random.randint(0, 2)

Possible:

    0
    1

Simulate a die:

    np.random.randint(1, 7)

Possible:

    1
    2
    3
    4
    5
    6

---

# 106. 🪙 Coin Toss

Example:

    np.random.seed(123)

    coin = np.random.randint(0, 2)

    if coin == 0:
        print("heads")
    else:
        print("tails")

---

# 107. 🎲 Empire State Building Game Rules

For each die roll:

| Roll | Action |
|---|---|
| `1` or `2` | Move down 1 |
| `3`, `4`, `5` | Move up 1 |
| `6` | Roll again, move up by second roll |

Additional rules:

- Never go below `0`.
- There is a chance of falling.
- Falling resets `step` to `0`.
- The goal is to reach at least `60`.

---

# 108. 🎯 Determine Next Step

    step = 50

    dice = np.random.randint(1, 7)

    if dice <= 2:
        step = step - 1
    elif dice <= 5:
        step = step + 1
    else:
        step = step + np.random.randint(1, 7)

---

# 109. 🛑 Prevent Step Below Zero

Use `max()`:

    step = max(0, step - 1)

Examples:

    max(0, 4)

returns:

    4

    max(0, -1)

returns:

    0

General pattern:

    variable = max(minimum_value, calculation)

---

# 110. 🚶 Random Walk

A random walk is a sequence of random steps where each new position depends on the previous position.

Basic pattern:

    random_walk = [0]

    for x in range(100):
        step = random_walk[-1]

        # calculate next step

        random_walk.append(step)

---

# 111. 🔙 Current Position of a Random Walk

Use:

    random_walk[-1]

This always selects the latest position.

Example:

    random_walk = [0, 2, 4, 3]

    random_walk[-1]

returns:

    3

---

# 112. 🧱 Build a Random Walk

    random_walk = [0]

    for x in range(100):
        step = random_walk[-1]
        dice = np.random.randint(1, 7)

        if dice <= 2:
            step = max(0, step - 1)
        elif dice <= 5:
            step = step + 1
        else:
            step = step + np.random.randint(1, 7)

        random_walk.append(step)

---

# 113. 📈 Visualize a Random Walk

Import Matplotlib:

    import matplotlib.pyplot as plt

Plot:

    plt.plot(random_walk)

Display:

    plt.show()

With one list, Matplotlib automatically uses:

- index → x-axis
- value → y-axis

---

# 114. 🧑‍🤝‍🧑 Multiple Random Walks

Store multiple walks:

    all_walks = []

    for i in range(5):
        random_walk = [0]

        for x in range(100):
            ...
            random_walk.append(step)

        all_walks.append(random_walk)

---

# 115. 📦 List of Lists → NumPy Array

    np_aw = np.array(all_walks)

If there are:

    5 walks
    101 positions per walk

then:

    np_aw.shape

is:

    (5, 101)

---

# 116. 🔄 Transpose

Transpose:

    np_aw_t = np.transpose(np_aw)

Shape changes:

    (5, 101)

to:

    (101, 5)

The rows and columns are swapped.

---

# 117. 📈 Plot All Walks

    plt.plot(np_aw_t)
    plt.show()

With the transposed array:

- Each column represents one random walk.
- Each line in the graph represents one walk.

---

# 118. 🧹 Clear a Matplotlib Figure

    plt.clf()

This clears the current figure.

Useful before plotting a new graph.

---

# 119. 🤕 Implement Clumsiness

Generate a random float:

    np.random.rand()

For a `0.5%` chance:

    if np.random.rand() <= 0.005:
        step = 0

For a `0.1%` chance:

    if np.random.rand() <= 0.001:
        step = 0

Remember:

    0.5% = 0.005
    0.1% = 0.001

---

# 120. 🏢 Full Random Walk with Clumsiness

    all_walks = []

    for i in range(20):
        random_walk = [0]

        for x in range(100):
            step = random_walk[-1]
            dice = np.random.randint(1, 7)

            if dice <= 2:
                step = max(0, step - 1)
            elif dice <= 5:
                step = step + 1
            else:
                step = step + np.random.randint(1, 7)

            if np.random.rand() <= 0.005:
                step = 0

            random_walk.append(step)

        all_walks.append(random_walk)

    np_aw_t = np.transpose(np.array(all_walks))

    plt.plot(np_aw_t)
    plt.show()

---

# 121. 📊 Distribution of Final Positions

A single random walk produces one final position.

Multiple random walks produce many final positions.

These final positions form a **distribution**.

Example:

    ends = [42, 57, 63, 48, 51, 60, ...]

---

# 122. 🎯 Extract Endpoints

If:

    np_aw_t.shape

is:

    (101, 500)

then:

    ends = np_aw_t[-1, :]

selects:

- Last row → final position
- All columns → all 500 walks

---

# 123. 📊 Histogram of Endpoints

    plt.hist(ends)
    plt.show()

This visualizes the distribution of final positions.

---

# 124. 🔬 Simulate Many Walks

Basic structure:

    final_results = []

    for i in range(number_of_simulations):
        # build one random walk
        ...
        final_results.append(random_walk[-1])

---

# 125. 🪙 Random Walk Example with Coin Tosses

A coin:

    0 → heads
    1 → tails

Track cumulative tails:

    tails = [0]

    for i in range(10):
        coin = np.random.randint(0, 2)
        tails.append(tails[-1] + coin)

The final value:

    tails[-1]

is the number of tails after 10 tosses.

---

# 126. 🔢 Why `tails[-1] + coin`?

If:

    coin = 0

then:

    tails[-1] + 0

does not change the total.

If:

    coin = 1

then:

    tails[-1] + 1

increases the total by one.

This converts random coin outcomes into a cumulative random walk.

---

# 127. 🧪 Simulating 10,000 Games

    final_tails = []

    for i in range(10000):
        tails = [0]

        for j in range(10):
            coin = np.random.randint(0, 2)
            tails.append(tails[-1] + coin)

        final_tails.append(tails[-1])

---

# 128. 📈 Histogram of a Distribution

    plt.hist(final_tails, bins=10)
    plt.show()

With more simulations:

    100
    1000
    10000

the simulated distribution becomes more stable and tends to approach the theoretical distribution.

---

# 129. 🎯 Calculate the Odds

Suppose:

    ends

contains 500 final positions.

To calculate the fraction reaching at least 60:

    np.mean(ends >= 60)

Why it works:

    True  → 1
    False → 0

Therefore, the mean of the Boolean array is the proportion of successful simulations.

---

# 130. ✅ Count-and-Divide Method

Equivalent calculation:

    len(ends[ends >= 60]) / 500

Or, more generally:

    len(ends[ends >= 60]) / len(ends)

---

# 131. 📊 Empire State Building Result

With the simulation settings you supplied:

- 500 random walks
- 100 dice throws per walk
- 0.1% falling chance
- Seed `123`

the estimated result was:

    0.784

As a percentage:

    78.4%

This means:

> 78.4% of the 500 simulated random walks reached at least step 60.

This is an **empirical simulation estimate**, not an exact analytical probability.

---

# 132. 📐 Probability Formula

General simulation estimate:

    probability =
        successful_simulations / total_simulations

Example:

    392 / 500

=

    0.784

=

    78.4%

---

# 133. 🧠 Boolean Mean Trick

Very useful NumPy pattern:

    np.mean(condition)

Examples:

    np.mean(cars["cars_per_cap"] > 500)

    np.mean(ends >= 60)

    np.mean(my_house >= 18)

This gives the proportion of values satisfying the condition.

---

# 134. 📚 Most Important Pandas Patterns

## Select one column

    df["column"]

## Select multiple columns

    df[["column1", "column2"]]

## Filter rows

    df[df["column"] > value]

## Multiple conditions

    df[
        np.logical_and(
            df["column1"] > value1,
            df["column2"] < value2
        )
    ]

## `loc`

    df.loc[row_label, "column"]

## `iloc`

    df.iloc[row_position, column_position]

## Iterate rows

    for label, row in df.iterrows():
        ...

## Apply function

    df["new_column"] = df["column"].apply(function)

---

# 135. 📚 Most Important NumPy Patterns

## Create array

    np.array([1, 2, 3])

## 2D array

    np.array([
        [1, 2],
        [3, 4]
    ])

## Shape

    array.shape

## Mean

    np.mean(array)

## Median

    np.median(array)

## Boolean filtering

    array[array > 10]

## Logical AND

    np.logical_and(condition1, condition2)

## Logical OR

    np.logical_or(condition1, condition2)

## Logical NOT

    np.logical_not(condition)

## Iterate every element

    np.nditer(array)

## Transpose

    np.transpose(array)

---

# 136. 📚 Most Important Matplotlib Patterns

## Import

    import matplotlib.pyplot as plt

## Line plot

    plt.plot(x, y)
    plt.show()

## One-list plot

    plt.plot(values)
    plt.show()

## Scatter

    plt.scatter(x, y)
    plt.show()

## Histogram

    plt.hist(values)
    plt.show()

## Histogram with bins

    plt.hist(values, bins=10)
    plt.show()

## Labels

    plt.xlabel("X")
    plt.ylabel("Y")

## Title

    plt.title("Title")

## Clear figure

    plt.clf()

---

# 137. 📚 Most Important Python Control Flow

## `if`

    if condition:
        ...

## `if-else`

    if condition:
        ...
    else:
        ...

## `if-elif-else`

    if condition1:
        ...
    elif condition2:
        ...
    else:
        ...

## `while`

    while condition:
        ...

## `for`

    for item in sequence:
        ...

## `enumerate`

    for index, item in enumerate(sequence):
        ...

---

# 138. 📚 Most Important Random Functions

## Seed

    np.random.seed(123)

## Random float

    np.random.rand()

## Random integer

    np.random.randint(1, 7)

## Simulate coin

    np.random.randint(0, 2)

## Simulate die

    np.random.randint(1, 7)

---

# 139. 🚨 Common Python Pitfalls

## `=` vs `==`

Wrong for comparison:

    if x = 5:

Correct:

    if x == 5:

---

## `<=` vs `=<`

Correct:

    x <= 5

Incorrect:

    x =< 5

---

## String Case Sensitivity

    "Python" == "python"

returns:

    False

---

## Missing Colon

Wrong:

    if x > 5
        print(x)

Correct:

    if x > 5:
        print(x)

---

## Incorrect Indentation

Wrong:

    if x > 5:
    print(x)

Correct:

    if x > 5:
        print(x)

---

## Infinite `while` Loop

Danger:

    while x > 0:
        print(x)

without changing `x`.

---

## Python `and` with NumPy Arrays

Avoid:

    (array > 5) and (array < 10)

Use:

    np.logical_and(array > 5, array < 10)

---

## Wrong `randint()` Upper Bound

For a six-sided die:

Wrong:

    np.random.randint(1, 6)

This gives only:

    1, 2, 3, 4, 5

Correct:

    np.random.randint(1, 7)

---

## DataFrame Row Iteration

This:

    for row in df:

does not iterate over rows.

It iterates over column names.

Use:

    for label, row in df.iterrows():

---

# 140. 🧠 Python Mental Models

## List

> Ordered collection of values.

    [10, 20, 30]

## NumPy Array

> Efficient numerical array.

    np.array([10, 20, 30])

## Dictionary

> Key-value mapping.

    {"country": "Philippines"}

## Pandas Series

> One labeled column.

    df["country"]

## Pandas DataFrame

> Two-dimensional labeled table.

    df

---

# 141. 🔄 Choosing the Right Tool

| Task | Recommended Tool |
|---|---|
| Store ordered values | List |
| Numerical calculations | NumPy array |
| Key-value mapping | Dictionary |
| Tabular data | Pandas DataFrame |
| One DataFrame column | Pandas Series |
| Plot numerical data | Matplotlib |
| Repeat until condition changes | `while` |
| Process every item | `for` |
| Row iteration | `iterrows()` |
| Whole-column transformation | `.apply()` / vectorized operations |
| Boolean NumPy logic | `np.logical_*()` |
| Random integer | `np.random.randint()` |
| Random float | `np.random.rand()` |

---

# 142. 🚀 High-Value Patterns to Memorize

## Boolean Filtering

    df[df["column"] > value]

## Multiple Conditions

    df[
        np.logical_and(
            df["column"] > lower,
            df["column"] < upper
        )
    ]

## Proportion Matching a Condition

    np.mean(df["column"] > value)

## Last List Element

    my_list[-1]

## Append

    my_list.append(value)

## Enumerate

    for index, value in enumerate(my_list):
        ...

## Dictionary Key-Value Iteration

    for key, value in my_dict.items():
        ...

## NumPy Element Iteration

    for value in np.nditer(array):
        ...

## DataFrame Row Iteration

    for label, row in df.iterrows():
        ...

## Apply Function

    df["new"] = df["old"].apply(function)

## Random Walk

    walk = [0]

    for i in range(100):
        step = walk[-1]
        # update step
        walk.append(step)

## Multiple Random Walks

    all_walks = []

    for i in range(number_of_walks):
        random_walk = [0]

        for j in range(number_of_steps):
            # update walk
            random_walk.append(step)

        all_walks.append(random_walk)

## Endpoint of Every Walk

    np_aw_t[-1, :]

## Simulation Probability

    np.mean(ends >= 60)

---

# 143. 🎯 Quick Reference — Operators

| Operator | Meaning |
|---|---|
| `+` | Add |
| `-` | Subtract |
| `*` | Multiply |
| `/` | Divide |
| `//` | Floor division |
| `%` | Remainder |
| `**` | Power |
| `=` | Assign |
| `==` | Equal |
| `!=` | Not equal |
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than/equal |
| `>=` | Greater than/equal |
| `and` | Both true |
| `or` | At least one true |
| `not` | Reverse Boolean |

---

# 144. 🎯 Quick Reference — Indexing

Given:

    values = [10, 20, 30, 40, 50]

| Expression | Result |
|---|---|
| `values[0]` | `10` |
| `values[1]` | `20` |
| `values[-1]` | `50` |
| `values[:2]` | `[10, 20]` |
| `values[1:4]` | `[20, 30, 40]` |
| `values[2:]` | `[30, 40, 50]` |
| `values[-2:]` | `[40, 50]` |

---

# 145. 🎯 Quick Reference — Boolean Logic

| A | B | `A and B` | `A or B` |
|---|---|---|---|
| `True` | `True` | `True` | `True` |
| `True` | `False` | `False` | `True` |
| `False` | `True` | `False` | `True` |
| `False` | `False` | `False` | `False` |

    not True   # False
    not False  # True

---

# 146. 🎯 Quick Reference — NumPy Logical Operations

    np.logical_and(a, b)

    np.logical_or(a, b)

    np.logical_not(a)

Use these when working with Boolean NumPy arrays or Pandas Series.

---

# 147. 🎯 Quick Reference — Loop Types

## List

    for value in values:
        print(value)

## List + index

    for index, value in enumerate(values):
        print(index, value)

## Dictionary

    for key, value in dictionary.items():
        print(key, value)

## NumPy 1D

    for value in array:
        print(value)

## NumPy multidimensional

    for value in np.nditer(array):
        print(value)

## DataFrame rows

    for label, row in df.iterrows():
        print(label, row)

---

# 148. 🎯 Quick Reference — Pandas

    import pandas as pd

    df = pd.read_csv("file.csv", index_col=0)

    df["column"]

    df[["column1", "column2"]]

    df.loc[row_label, "column"]

    df.iloc[row_position, column_position]

    df[df["column"] > 10]

    df["new_column"] = df["column"].apply(len)

    for label, row in df.iterrows():
        print(row["column"])

---

# 149. 🎯 Quick Reference — Random Walk

    import numpy as np
    import matplotlib.pyplot as plt

    np.random.seed(123)

    random_walk = [0]

    for i in range(100):
        step = random_walk[-1]
        dice = np.random.randint(1, 7)

        if dice <= 2:
            step = max(0, step - 1)
        elif dice <= 5:
            step += 1
        else:
            step += np.random.randint(1, 7)

        if np.random.rand() <= 0.001:
            step = 0

        random_walk.append(step)

    plt.plot(random_walk)
    plt.show()

---

# 150. 🎯 Quick Reference — Multiple Random Walks

    all_walks = []

    for i in range(500):
        random_walk = [0]

        for j in range(100):
            step = random_walk[-1]
            dice = np.random.randint(1, 7)

            if dice <= 2:
                step = max(0, step - 1)
            elif dice <= 5:
                step += 1
            else:
                step += np.random.randint(1, 7)

            if np.random.rand() <= 0.001:
                step = 0

            random_walk.append(step)

        all_walks.append(random_walk)

    np_aw_t = np.transpose(np.array(all_walks))

    ends = np_aw_t[-1, :]

    plt.hist(ends)
    plt.show()

---

# 151. 🎯 Quick Reference — Calculate Simulation Odds

Count successful endpoints:

    len(ends[ends >= 60])

Divide by number of simulations:

    len(ends[ends >= 60]) / len(ends)

Or use the Boolean mean:

    np.mean(ends >= 60)

Convert to percentage:

    np.mean(ends >= 60) * 100

Example result from the supplied simulation:

    0.784

    78.4%

---

# 152. 🧠 Final Mental Checklist

When solving Python data-analysis exercises, ask:

### 1. What data structure am I using?

    list
    dictionary
    NumPy array
    Series
    DataFrame

### 2. Am I selecting or modifying?

Selecting:

    x[index]
    df["column"]

Modifying:

    x[index] = value
    df["new"] = ...

### 3. Do I need a loop?

If processing each item:

    for ...

If repeating until a condition changes:

    while ...

If the operation applies to an entire Pandas column:

    apply()
    vectorized operation

### 4. Do I need Boolean logic?

Single value:

    and
    or
    not

NumPy/Pandas arrays:

    np.logical_and()
    np.logical_or()
    np.logical_not()

### 5. Do I need random numbers?

Float:

    np.random.rand()

Integer:

    np.random.randint(low, high)

Reproducibility:

    np.random.seed(123)

### 6. Am I analyzing a distribution?

Collect final results:

    results.append(final_value)

Visualize:

    plt.hist(results)

Estimate probability:

    np.mean(condition)

---

# 🏆 Final Cheat Sheet Summary

## Python Fundamentals

    variable = value
    type(value)
    print(value)
    len(value)

## Lists

    values[index]
    values[start:end]
    values.append(value)
    values.extend(other_list)
    values.pop()
    del values[index]

## Conditions

    if condition:
        ...

    elif condition:
        ...

    else:
        ...

## Loops

    for item in sequence:
        ...

    for index, item in enumerate(sequence):
        ...

    while condition:
        ...

## Dictionaries

    dictionary[key]
    dictionary.items()
    dictionary.keys()
    dictionary.values()

## NumPy

    np.array(...)
    array.shape
    np.mean(...)
    np.median(...)
    np.logical_and(...)
    np.logical_or(...)
    np.logical_not(...)
    np.nditer(...)
    np.transpose(...)

## Pandas

    pd.read_csv(...)
    df["column"]
    df[["column1", "column2"]]
    df.loc[...]
    df.iloc[...]
    df[condition]
    df.iterrows()
    df["new"] = df["old"].apply(function)

## Matplotlib

    plt.plot(...)
    plt.scatter(...)
    plt.hist(...)
    plt.xlabel(...)
    plt.ylabel(...)
    plt.title(...)
    plt.xticks(...)
    plt.grid(...)
    plt.clf()
    plt.show()

## Random Simulation

    np.random.seed(123)
    np.random.rand()
    np.random.randint(1, 7)

## Random Walk

    random_walk = [0]
    step = random_walk[-1]
    random_walk.append(step)

## Probability from Simulation

    np.mean(results >= target)

---

# 🚀 Most Important Things to Remember

> 🔹 `=` assigns, `==` compares.

> 🔹 Python indexes start at `0`.

> 🔹 `list[-1]` gets the last element.

> 🔹 `start:end` excludes `end`.

> 🔹 `and`, `or`, `not` work with ordinary Boolean values.

> 🔹 `np.logical_and()`, `np.logical_or()`, `np.logical_not()` are used for NumPy/Pandas Boolean arrays.

> 🔹 `if` checks once; `while` repeats while true; `for` iterates over a sequence.

> 🔹 `enumerate()` gives index + value.

> 🔹 `.items()` gives dictionary key + value.

> 🔹 `np.nditer()` iterates through every element of a multidimensional NumPy array.

> 🔹 `iterrows()` iterates through Pandas rows.

> 🔹 `.apply()` is useful for applying a function to a Pandas Series.

> 🔹 `np.random.randint(1, 7)` simulates a six-sided die.

> 🔹 `np.random.seed()` makes pseudo-random simulations reproducible.

> 🔹 A random walk stores cumulative positions, not just independent random outcomes.

> 🔹 A distribution of final random-walk positions can be visualized with a histogram.

> 🔹 `np.mean(condition)` is a powerful way to calculate the proportion of observations satisfying a Boolean condition.
