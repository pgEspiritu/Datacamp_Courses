# 🧩 Methods

Built-in functions are only one part of Python. Python also provides **methods**, which are functions that belong to specific Python objects.

## 📌 Built-in Functions vs. Methods

You have already used built-in functions such as:

    max()
    len()
    type()
    round()

These functions are called directly.

Methods, on the other hand, are called **on an object** using dot notation:

    object.method()

### Example

    fam.index("mom")

Here, `index()` is a method that belongs to the `fam` list.

---

# 🐍 Python Objects

In Python, values and data structures are represented as **objects**.

Examples:

    "liz"              # string object
    1.73               # float object
    [1.73, 1.68]       # list object

Each object has a specific **type**.

| Object | Type |
|---|---|
| `"liz"` | `str` |
| `1.73` | `float` |
| `[1.73, 1.68]` | `list` |

Objects also have methods associated with their type.

## 💡 What Is a Method?

A **method** is a function that belongs to an object.

You can think of it as:

    object.method()

The available methods depend on the object's type.

For example:

- 📋 Lists have list methods.
- 🔤 Strings have string methods.
- 🔢 Numeric objects have their own methods.

---

# 📋 List Methods

Suppose:

    fam = ["liz", 1.73, "emma", 1.68, "mom", 1.65]

## 🔍 `index()`

The `index()` method finds the position of an element in a list.

    fam.index("mom")

Output:

    4

The `"mom"` element is located at index `4`.

### 📌 Syntax

    list.index(value)

---

## 🔢 `count()`

The `count()` method counts how many times a value appears in a list.

    fam.count(1.73)

Output:

    1

The value `1.73` appears once in the list.

### 📌 Syntax

    list.count(value)

---

# 🔤 String Methods

Strings are also Python objects and have their own methods.

Suppose:

    sister = "liz"

## 🔠 `capitalize()`

The `capitalize()` method makes the first character uppercase.

    sister.capitalize()

Output:

    "Liz"

The original string is not changed by this method call.

---

## 🔄 `replace()`

The `replace()` method replaces part of a string with another value.

For example:

    sister.replace("z", "sa")

Output:

    "lisa"

### 📌 Syntax

    string.replace(old, new)

The two arguments specify:

- `old` → text to replace
- `new` → replacement text

---

# ⚠️ Methods Depend on Object Type

Different Python objects have different methods.

For example:

    fam.replace("a", "b")

will produce an error because lists do not have a `replace()` method.

However:

    sister.replace("z", "sa")

works because strings have a `replace()` method.

### 💡 Key Idea

The **type of the object determines which methods are available**.

---

# 🔁 Same Method Name, Different Behavior

Different object types can have methods with the same name.

For example, both lists and strings have an `index()` method.

### List

    fam.index("mom")

This returns the index of an **element in the list**.

### String

    sister.index("z")

This returns the index of a **character in the string**.

So, the same method name can behave differently depending on the type of object it is called on.

---

# ➕ Methods That Modify Objects

Some methods **change the object they are called on**.

For example, the `append()` method adds an element to a list.

Suppose:

    fam = ["liz", 1.73, "emma", 1.68]

You can add `"mom"` using:

    fam.append("mom")

The list is now:

    ["liz", 1.73, "emma", 1.68, "mom"]

You can add another value:

    fam.append(1.65)

The list becomes:

    ["liz", 1.73, "emma", 1.68, "mom", 1.65]

## ⚠️ Important

The `append()` method changes the original list.

It does not create a separate list.

This is different from methods that simply return a result without changing the original object.

### Example

    sister.capitalize()

returns a new string value, but does not change `sister`.

Meanwhile:

    fam.append("mom")

changes the original `fam` list.

---

# 🧠 Functions vs. Methods

## Functions

Functions are called directly:

    type(fam)
    max(fam)
    round(1.68, 1)

## Methods

Methods are called using dot notation:

    fam.index("mom")
    fam.count(1.73)
    fam.append("mom")
    sister.capitalize()
    sister.replace("z", "sa")

### 🔍 Comparison

| Feature | Function | Method |
|---|---|---|
| Called directly | ✅ | ❌ |
| Called using dot notation | ❌ | ✅ |
| Associated with a specific object | ❌ | ✅ |
| Example | `max(fam)` | `fam.index("mom")` |

---

# 🎯 Common Methods

| Object Type | Method | Purpose | Example |
|---|---|---|---|
| `list` | `index()` | Find the index of an element | `fam.index("mom")` |
| `list` | `count()` | Count occurrences | `fam.count(1.73)` |
| `list` | `append()` | Add an element | `fam.append("mom")` |
| `str` | `capitalize()` | Capitalize the first character | `sister.capitalize()` |
| `str` | `replace()` | Replace text | `sister.replace("z", "sa")` |

---

# 📌 Dot Notation

Methods are called using **dot notation**:

    object.method()

Examples:

    fam.index("mom")
    fam.count(1.73)
    fam.append("mom")
    sister.capitalize()
    sister.replace("z", "sa")

The object comes first, followed by a dot `.`, then the method name.

---

# 💡 Key Takeaways

- 🧩 A **method** is a function associated with a Python object.
- 🐍 Python objects have different types, such as `list`, `str`, and `float`.
- 🔗 Methods are called using **dot notation**: `object.method()`.
- 📋 Lists have methods such as `index()`, `count()`, and `append()`.
- 🔤 Strings have methods such as `capitalize()` and `replace()`.
- 🔄 The same method name can behave differently for different object types.
- ⚠️ Some methods modify the original object, while others return a result without modifying it.
- 🧠 Always consider the object's **type** when determining which methods are available.
- 🚀 Understanding methods makes it easier to work efficiently with Python objects.
