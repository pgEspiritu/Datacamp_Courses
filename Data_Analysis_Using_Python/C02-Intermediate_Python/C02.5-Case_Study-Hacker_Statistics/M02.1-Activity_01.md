# 🚶 Random Walk in Python

## 📌 Overview

A **random walk** is a sequence of random steps where the current position is updated based on the outcome of each step.

If you use a die once to determine your next movement, that is a **random step**.

If you use the die repeatedly, for example `100` times, you get a succession of random steps. This is called a:

> **Random walk**

Random walks are useful for modeling many real-world processes.

Examples include:

- The movement of molecules in liquids or gases
- The financial status of a gambler
- Other processes involving repeated random changes

---

# 🎲 Random Step vs Random Walk

### Random Step

A single random outcome determines one movement.

Example:

    die = np.random.randint(1, 7)

### Random Walk

Multiple random outcomes determine a sequence of positions:

    step 1 → step 2 → step 3 → step 4 → ...

The important difference is that a random walk **tracks the changing position over time**.

---

# 🪙 Example: Heads or Tails

Suppose we play a coin-toss game `10` times.

We can use:

    np.random.randint(0, 2)

to generate either:

    0 → Heads
    1 → Tails

---

# 🧱 Building a List with a `for` Loop

To record the result of every coin toss, start with an empty list:

    outcomes = []

Then use a `for` loop that runs `10` times.

The `range()` function can generate the sequence used to control the loop:

    for i in range(10):
        ...

---

# 🔢 `range()`

The expression:

    range(10)

generates values corresponding to:

    0, 1, 2, 3, 4, 5, 6, 7, 8, 9

This gives the loop **10 iterations**.

You usually do not need to use the values from `range()` directly; it can simply control how many times the loop executes.

---

# 🪙 Simulating 10 Coin Tosses

The basic process is:

1. Start with an empty list.
2. Repeat the experiment `10` times.
3. Generate a random coin result.
4. Add `"heads"` or `"tails"` to the list.
5. Print the completed list.

### Example

    import numpy as np

    np.random.seed(123)

    outcomes = []

    for i in range(10):
        coin = np.random.randint(0, 2)

        if coin == 0:
            outcomes.append("heads")
        else:
            outcomes.append("tails")

    print(outcomes)

---

# 📌 Using `.append()`

The `.append()` method adds an item to the end of a list.

Example:

    outcomes = []

    outcomes.append("heads")
    outcomes.append("tails")

The list becomes:

    ["heads", "tails"]

In the coin-toss example:

    outcomes.append("heads")

or:

    outcomes.append("tails")

adds the current result to the list.

---

# 🧠 Why This Is Not Yet a Random Walk

The `outcomes` list contains a sequence such as:

    ["heads", "tails", "tails", "heads", ...]

These are random results, but they are **not a random walk**.

Why?

Because the result of one toss does not determine or update a position based on the previous result.

It is simply a collection of independent random outcomes.

---

# 🚶 Turning Coin Tosses into a Random Walk

To turn the coin-toss experiment into a random walk, we need to track a **running total**.

In this example, we'll track the total number of times `"tails"` has occurred.

Start with:

    tails = [0]

The initial `0` means:

> At the beginning, we have seen zero tails.

---

# 🔄 Building the Random Walk

We again use a loop that runs `10` times:

    for i in range(10):
        coin = np.random.randint(0, 2)

Then update the number of tails.

Remember:

    0 → Heads
    1 → Tails

If the result is `0`, the number of tails should not change.

If the result is `1`, the number of tails should increase by `1`.

Instead of using an `if-else` statement, we can directly add `coin` to the previous total.

---

# ✅ Random Walk Example

    import numpy as np

    np.random.seed(123)

    tails = [0]

    for i in range(10):
        coin = np.random.randint(0, 2)
        tails.append(tails[-1] + coin)

    print(tails)

---

# 🧠 Understanding `tails[-1]`

The expression:

    tails[-1]

selects the **last element** in the list.

For example:

    tails = [0, 1, 1, 2]

Then:

    tails[-1]

is:

    2

This lets us take the previous total and update it.

---

# ➕ Updating the Tails Count

The expression:

    tails[-1] + coin

means:

> Take the previous number of tails and add the latest coin result.

### If `coin == 0`

    tails[-1] + 0

The number of tails stays the same.

### If `coin == 1`

    tails[-1] + 1

The number of tails increases by one.

Then:

    tails.append(tails[-1] + coin)

adds the new total to the list.

---

# 📊 Why Does `tails` Have 11 Elements?

The list begins with:

    tails = [0]

So there is already **one element** representing the starting position.

Then the loop runs `10` times.

Each iteration adds one new value.

Therefore:

    1 initial value + 10 new values = 11 values

The resulting list might look like:

    [0, 1, 1, 2, 3, 3, 4, 5, 5, 6, 6]

The exact values depend on the random sequence.

---

# 🔍 Example of the Random Walk

Suppose the coin results are:

    1, 0, 1, 1, 0

These correspond to:

    Tails, Heads, Tails, Tails, Heads

Starting with:

    tails = [0]

The running totals become:

    0
    1
    1
    2
    3
    3

The list records the **position after every step**.

---

# 🆚 Random Outcomes vs Random Walk

## Random Outcomes

    outcomes = []

    for i in range(10):
        coin = np.random.randint(0, 2)

        if coin == 0:
            outcomes.append("heads")
        else:
            outcomes.append("tails")

The list stores the individual events:

    ["heads", "tails", "tails", ...]

---

## Random Walk

    tails = [0]

    for i in range(10):
        coin = np.random.randint(0, 2)
        tails.append(tails[-1] + coin)

The list stores the **cumulative position**:

    [0, 1, 1, 2, 3, ...]

The second list is a random walk because every new value depends on the previous position.

---

# 🧠 The Key Difference

### Random Sequence

Each result is simply another random outcome.

    outcome → random
    outcome → random
    outcome → random

### Random Walk

Each new position builds on the previous position.

    position₀
       ↓
    position₁
       ↓
    position₂
       ↓
    position₃

This cumulative behavior is what turns random steps into a random walk.

---

# 🔄 Random Walk Pattern

A common pattern for building a random walk is:

    positions = [starting_position]

    for i in range(number_of_steps):
        random_step = ...
        positions.append(positions[-1] + random_step)

The key components are:

- A starting position
- A loop that generates random steps
- The previous position
- A new position based on the random step
- `.append()` to save every position

---

# 📚 Important Python Concepts Used

This lesson combines several concepts learned earlier:

### `np.random.randint()`

Generates random integers:

    coin = np.random.randint(0, 2)

### `range()`

Controls the number of loop iterations:

    for i in range(10):

### `if-else`

Can classify the random outcome:

    if coin == 0:
        ...
    else:
        ...

### `.append()`

Adds a new item to a list:

    outcomes.append("heads")

### Negative Indexing

Access the last list element:

    tails[-1]

### `for` Loop

Repeats the random process:

    for i in range(10):
        ...

---

# 🔑 Key Takeaways

- A **random step** is one random movement.
- A **random walk** is a sequence of random steps.
- `range()` is useful for repeating an experiment a fixed number of times.
- `.append()` can gradually build a list during a `for` loop.
- A list can start with an initial position:

      tails = [0]

- `tails[-1]` accesses the current/latest position.
- Updating the list with:

      tails.append(tails[-1] + coin)

  creates a cumulative random walk.
- The final element of the random-walk list represents the **final position** after all steps.

### 📚 Core Pattern

    positions = [0]

    for i in range(10):
        step = np.random.randint(0, 2)
        positions.append(positions[-1] + step)

> 🎯 **Core idea:** A random walk is created by repeatedly generating random steps and adding each step to the previous position.
