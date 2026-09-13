# 🛠️ Manipulating Lists

After **creating** and **subsetting** lists, the next step is learning how to **manipulate** them.

List manipulation includes:

- ✏️ Changing existing elements
- ➕ Adding elements
- ➖ Removing elements
- 📋 Copying lists correctly

## ✏️ Changing List Elements

You can change an element in a list using the same square brackets used for subsetting, followed by the assignment operator `=`.

### Example

Suppose the `fam` list contains your dad's height at index `7`.

If his height needs to be changed from `1.89` to `1.86`:

    fam[7] = 1.86

The value at index `7` is now updated.

### 🔄 Changing Multiple Elements

You can also replace an entire slice of a list.

For example, to replace the first two elements:

    fam[0:2] = ["liz", 1.74]

The slice `0:2` selects indexes `0` and `1`.

The new list replaces those elements.

### 📌 General Syntax

    list[index] = new_value

For multiple elements:

    list[start:end] = new_list

---

## ➕ Adding Elements to Lists

The `+` operator can be used to combine two lists.

Unlike adding numbers, using `+` with lists combines their contents into one list.

### Example

    fam + ["Gio", 1.75]

This creates a new list containing the original `fam` elements plus `"Gio"` and `1.75`.

You can store the result in another variable:

    fam_ext = fam + ["Gio", 1.75]

### 📌 General Syntax

    new_list = list1 + list2

The original lists are not modified when using `+`.

---

## ➖ Removing Elements from Lists

Use the `del` statement to remove an element from a list.

### Example

    del fam[2]

This removes the element at index `2`.

If index `2` contained `"emma"`, `"emma"` is removed from the list.

### ⚠️ Important

When an element is deleted, the elements after it **shift one position to the left**.

For example:

    Before deletion:

    Index    Element
    0        liz
    1        1.73
    2        emma
    3        1.68
    4        dad
    5        1.89

    After del fam[2]:

    Index    Element
    0        liz
    1        1.73
    2        1.68
    3        dad
    4        1.89

The element that was previously at index `3` becomes index `2`.

### 📌 General Syntax

    del list[index]

---

# 🧠 Behind the Scenes: How Python Lists Work

Understanding how Python handles lists becomes important when copying lists.

## 📍 Variables Store References

When you create a list:

    x = ["a", "b", "c"]

Python stores the list somewhere in computer memory.

The variable `x` contains a **reference** to that list.

In simplified terms:

    x ───────► ["a", "b", "c"]

The variable does not directly contain the list itself. It points to where the list is stored in memory.

---

## ⚠️ Copying a List with `=`

Suppose you create another variable using:

    y = x

It may look like you copied the list, but you actually copied the **reference**.

Both variables point to the same list:

    x ───────► ["a", "b", "c"]
                 ▲
                 │
    y ───────────┘

If you change the list through `y`:

    y[1] = "new"

The list becomes:

    ["a", "new", "c"]

Checking `x` will also show the change:

    print(x)

Output:

    ['a', 'new', 'c']

### 💡 Why?

Because `x` and `y` refer to the **same list in memory**.

Using:

    y = x

does **not** create an independent copy of the list.

---

# 📋 Creating an Independent Copy

If you want `y` to contain the same values but refer to a **different list**, you need to create a copy.

There are two common ways.

## Method 1: Use `list()`

    y = list(x)

This creates a new list with the same elements.

Conceptually:

    x ───────► ["a", "b", "c"]

    y ───────► ["a", "b", "c"]

The lists contain the same values, but they are separate lists.

Changing `y` will not change `x`:

    y[1] = "new"

Now:

    print(x)
    print(y)

Output:

    ['a', 'b', 'c']
    ['a', 'new', 'c']

---

## Method 2: Use List Slicing

You can also copy all elements using slicing:

    y = x[:]

The `[:]` slice selects the entire list and creates a new list.

Again, changes to `y` will not affect `x`.

---

# 🔍 Comparing List Copying Methods

| Method | Creates New List? | Changes to `y` Affect `x`? |
|---|---|---|
| `y = x` | ❌ No | ✅ Yes |
| `y = list(x)` | ✅ Yes | ❌ No |
| `y = x[:]` | ✅ Yes | ❌ No |

## ⚠️ Important Difference

### Reference Assignment

    y = x

Both variables point to the **same list**.

### Independent Copy

    y = list(x)

or:

    y = x[:]

The variables point to **different lists containing the same values**.

---

# 🎯 Quick Reference

### Change an element

    fam[7] = 1.86

### Change multiple elements

    fam[0:2] = ["liz", 1.74]

### Combine lists

    fam_ext = fam + ["Gio", 1.75]

### Delete an element

    del fam[2]

### Create a reference to the same list

    y = x

### Create an independent copy

    y = list(x)

or:

    y = x[:]

---

# 💡 Key Takeaways

- ✏️ Use `list[index] = value` to **change** an element.
- ✂️ Use `list[start:end] = new_list` to **replace multiple elements**.
- ➕ Use `+` to **combine lists**.
- ➖ Use `del` to **remove elements**.
- ⚠️ `y = x` copies the **reference**, not the actual list.
- 📋 `y = list(x)` creates a **new list**.
- ✂️ `y = x[:]` also creates a **new list**.
- 🧠 When using `y = x`, changes made through either variable affect the **same underlying list**.
- 🚀 Understanding references and copies is important when working with Python lists.
