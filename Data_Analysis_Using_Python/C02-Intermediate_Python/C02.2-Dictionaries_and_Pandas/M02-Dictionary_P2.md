# 📚 Dictionaries, Part 2 🗂️

## 🔄 Dictionary Recap

A Python dictionary is a collection of **key-value pairs**.

Example:

    world = {
        "afghanistan": 30.55,
        "albania": 2.77,
        "algeria": 40.00
    }

You can access a value using its key:

    world["albania"]

Result:

    2.77

---

# 🔑 Dictionary Keys Must Be Unique

Each dictionary key must be **unique**.

For example:

    world = {
        "albania": 2.77,
        "albania": 3.00
    }

The resulting dictionary will contain only one `"albania"` key.

The **last value assigned to the duplicate key** is kept:

    {
        "albania": 3.00
    }

Therefore:

⚠️ Avoid duplicate keys when creating dictionaries.

---

# 🔒 Dictionary Keys Must Be Immutable

Dictionary keys must be **immutable objects**.

An immutable object cannot be changed after it is created.

### ✅ Valid Dictionary Key Types

Common immutable types include:

- 🔤 Strings
- 🔢 Integers
- 🔢 Floats
- ✅ Booleans

Example:

    example = {
        "name": "Gio",
        25: "age",
        1.75: "height",
        True: "active"
    }

These are valid because their values cannot be modified in place.

---

# ❌ Lists Cannot Be Dictionary Keys

Lists are **mutable** because their contents can be changed.

Therefore, a list cannot be used as a dictionary key.

Invalid example:

    world = {
        ["spain", "france"]: "europe"
    }

This causes an error because a list is mutable and therefore cannot be used as a dictionary key.

### 💡 Remember

| Object Type | Mutable? | Can Be Dictionary Key? |
|---|---|---|
| String | ❌ No | ✅ Yes |
| Integer | ❌ No | ✅ Yes |
| Float | ❌ No | ✅ Yes |
| Boolean | ❌ No | ✅ Yes |
| List | ✅ Yes | ❌ No |

---

# ➕ Adding Data to a Dictionary

You can add a new key-value pair using square brackets and assignment.

Example:

    world["sealand"] = 27

This adds:

    "sealand": 27

to the dictionary.

---

# 🌍 Sealand Example

Suppose the World Bank dataset contains:

    world = {
        "afghanistan": 30.55,
        "albania": 2.77,
        "algeria": 40.00
    }

You decide to add the Principality of Sealand.

The population is:

    27 inhabitants

Represented in millions:

    0.000027

You can add it using:

    world["sealand"] = 0.000027

The dictionary now contains a new key-value pair.

---

# 🔎 Checking if a Key Exists

Python allows you to check whether a key exists in a dictionary using the `in` operator.

Example:

    "sealand" in world

Result:

    True

If the key does not exist:

    "japan" in world

Result:

    False

### 📌 General Syntax

    key in dictionary

This is useful when checking whether information already exists.

---

# ✏️ Updating Dictionary Values

The same syntax used to add new data can also update an existing value.

Example:

    world["sealand"] = 28

If `"sealand"` already exists, Python updates its value instead of creating a second key.

Before:

    "sealand": 27

After:

    "sealand": 28

Because dictionary keys are unique, Python knows that this is an **update**.

---

# 🗑️ Removing Dictionary Elements

Use the `del` statement to remove a key-value pair.

Example:

    del world["sealand"]

The `"sealand"` key and its corresponding value are removed from the dictionary.

After deletion:

    "sealand" in world

returns:

    False

---

# 📋 Lists vs Dictionaries

Lists and dictionaries have some similarities.

Both allow you to:

- 🔍 Select data
- ✏️ Update data
- 🗑️ Remove data

They both use square brackets for accessing or changing elements.

However, they are fundamentally different data structures.

---

# 📊 Lists

A list is a **sequence of values** indexed by numbers.

Example:

    countries = ["spain", "france", "germany"]

Access an element:

    countries[1]

Result:

    "france"

List indexes are based on positions:

    0 → first element
    1 → second element
    2 → third element

Lists are useful when:

✅ Order matters  
✅ You need positional indexing  
✅ You want to easily select slices or subsets  

---

# 🗂️ Dictionaries

A dictionary is indexed by **unique keys**.

Example:

    capitals = {
        "spain": "madrid",
        "france": "paris",
        "germany": "berlin"
    }

Access a value:

    capitals["france"]

Result:

    "paris"

The key itself identifies the value.

---

# ⚖️ List vs Dictionary Comparison

| Feature | List 📋 | Dictionary 🗂️ |
|---|---|---|
| Structure | Sequence of values | Key-value pairs |
| Indexing | Numeric indexes | Unique keys |
| Order | Important | Used primarily for key-based lookup |
| Keys | ❌ No | ✅ Yes |
| Fast key lookup | ❌ No | ✅ Yes |
| Slicing | ✅ Yes | ❌ Not the main use |
| Best for | Ordered collections | Lookup tables |

---

# 🧠 When Should You Use a List?

Choose a **list** when:

- 📋 You have a collection of values.
- 🔢 Position or order matters.
- ✂️ You need to select subsets or slices.
- 📊 You want sequential data.

Example:

    scores = [85, 90, 78, 92]

Access by position:

    scores[2]

Result:

    78

---

# 🧠 When Should You Use a Dictionary?

Choose a **dictionary** when:

- 🔑 Each value has a unique identifier.
- 🔎 You need fast lookups.
- 🗂️ Data naturally forms key-value relationships.
- 📊 You are building a lookup table.

Example:

    student_scores = {
        "Ana": 85,
        "Ben": 90,
        "Carla": 78
    }

Access directly using a key:

    student_scores["Ben"]

Result:

    90

---

# 🎯 Dictionary Operations Quick Reference

### Access a value

    world["albania"]

### Add a new key-value pair

    world["sealand"] = 27

### Update a value

    world["sealand"] = 28

### Check if a key exists

    "sealand" in world

### Delete a key-value pair

    del world["sealand"]

### Get all keys

    world.keys()

---

# 💡 Key Takeaways

- 🗂️ Dictionaries store **key-value pairs**.
- 🔑 Dictionary keys must be **unique**.
- 🔒 Dictionary keys must be **immutable**.
- ➕ Use `dictionary[key] = value` to add data.
- ✏️ Use the same syntax to update an existing value.
- 🗑️ Use `del dictionary[key]` to remove data.
- 🔎 Use `key in dictionary` to check whether a key exists.
- 📋 Use lists when **order and position** matter.
- 🗂️ Use dictionaries when you need **fast lookup using unique keys**.
- 🚀 Choosing the correct data structure makes Python programs easier to understand and more efficient.
