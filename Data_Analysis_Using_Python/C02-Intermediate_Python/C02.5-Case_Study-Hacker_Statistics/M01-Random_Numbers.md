# 🎲 Random Numbers in Python

## 📌 Overview

This chapter combines many of the Python concepts learned so far to build a simulation.

The goal is to simulate a game where you are walking up the **Empire State Building** while repeatedly rolling a die.

This type of simulation is an example of **Hacker Statistics**: instead of calculating probabilities entirely with mathematical formulas, we simulate the process many times and study the results.

---

# 🏢 Empire State Building Game

Imagine you're walking up the Empire State Building with a friend.

You throw a die **100 times**.

The rules are:

| Die Roll | Action |
|---|---|
| `1` or `2` | Go **1 step down** |
| `3`, `4`, or `5` | Go **1 step up** |
| `6` | Roll the die again and go up by the resulting number of steps |

There are also two additional rules:

- You can **never go below step `0`**.
- Each time you make a move, there is a **0.1% chance** of falling down the stairs.
- If you fall, you return to **step `0`**.

The bet is:

> Can you reach **60 steps high**?

---

# 📊 How Can We Calculate the Chance?

There are two broad approaches:

### Mathematical Approach

We could try to calculate the probability analytically using equations and probability theory.

### Simulation Approach

We can simulate the game **thousands of times** and calculate the fraction of simulations in which the player reaches step `60`.

This simulation-based approach is called:

> **Hacker Statistics**

Instead of solving the probability directly, we let the computer simulate many random outcomes and use those outcomes to estimate the probability.

---

# 🎲 Random Number Generators

To simulate a die, we need random numbers.

NumPy provides random-number functionality through its `random` package.

First import NumPy:

    import numpy as np

---

# 🔢 `np.random.rand()`

The `rand()` function generates a random floating-point number between `0` and `1`.

Example:

    np.random.rand()

A possible output might be:

    0.573921

Another call could produce a different value:

    0.184372

The generated values are **pseudo-random**.

---

# 🧠 What Does "Pseudo-Random" Mean?

Computers generally generate random-looking numbers using mathematical algorithms.

These are called **pseudo-random numbers** because:

- They appear random.
- They are generated according to a deterministic algorithm.
- The sequence can be reproduced when the same random seed is used.

This reproducibility is extremely useful in data analysis and simulations.

---

# 🌱 Random Seed

A **random seed** determines the starting point of the pseudo-random number generator.

NumPy allows you to set the seed using:

    np.random.seed()

For example:

    np.random.seed(123)

Then:

    np.random.rand()

generates a reproducible sequence of random values.

---

# 🔁 Reproducibility

Consider:

    np.random.seed(123)

    print(np.random.rand())
    print(np.random.rand())

Running this sequence produces the same two random numbers whenever the same seed is used.

If you reset the seed:

    np.random.seed(123)

and call:

    print(np.random.rand())
    print(np.random.rand())

you get the **same two values again**.

This means the random process is reproducible.

---

# 💡 Why Is Reproducibility Important?

Suppose you perform an analysis using random simulations.

If another person uses:

    np.random.seed(123)

and follows the same procedure, they can reproduce your results.

This is especially useful for:

- Data analysis
- Simulations
- Machine learning experiments
- Debugging
- Testing

> 🎯 **Same seed + same code = same pseudo-random sequence**

---

# 🪙 Simulating a Coin Toss

Random numbers can be used to simulate real-world events involving chance.

For a coin toss, we can use:

    np.random.randint()

---

# 🔢 `np.random.randint()`

The `randint()` function generates a random integer within a specified range.

For example:

    np.random.randint(0, 2)

generates either:

    0

or:

    1

### Important

The first argument is **included**.

The second argument is **excluded**.

Therefore:

    np.random.randint(0, 2)

means:

    0 <= result < 2

Possible values:

    0
    1

---

# 🪙 Coin Toss Example

Set the seed first:

    np.random.seed(123)

Then generate the coin toss:

    coin = np.random.randint(0, 2)

Print it:

    print(coin)

A possible result is:

    0

We can interpret:

    0 → Heads
    1 → Tails

---

# 🧠 Using `if-else` with the Coin Toss

We can combine random numbers with conditional statements.

    np.random.seed(123)

    coin = np.random.randint(0, 2)

    if coin == 0:
        print("heads")
    else:
        print("tails")

If:

    coin = 0

the condition:

    coin == 0

is `True`, so Python prints:

    heads

If:

    coin = 1

the `else` block runs:

    tails

---

# 🔄 Randomness + Conditional Logic

This example combines concepts learned earlier:

### Random Number

    coin = np.random.randint(0, 2)

### Comparison

    coin == 0

### Conditional Statement

    if coin == 0:
        print("heads")
    else:
        print("tails")

This demonstrates how random numbers can be used to simulate events involving probability.

---

# 🎲 `rand()` vs `randint()`

| Function | Purpose | Example |
|---|---|---|
| `np.random.rand()` | Random floating-point number between `0` and `1` | `np.random.rand()` |
| `np.random.randint()` | Random integer in a specified range | `np.random.randint(0, 2)` |

### `rand()`

    np.random.rand()

Possible output:

    0.417022

### `randint()`

    np.random.randint(0, 2)

Possible output:

    0

or:

    1

---

# 🧠 Inclusive vs Exclusive Bounds

For:

    np.random.randint(0, 2)

the possible values are:

    0
    1

The upper bound `2` is **not included**.

This is an important rule:

> `randint(low, high)` includes `low` but excludes `high`.

For example:

    np.random.randint(1, 7)

produces a random integer from:

    1
    2
    3
    4
    5
    6

This is exactly what we need to simulate a six-sided die.

---

# 🎯 Simulating a Die

A standard die produces integers from `1` to `6`.

Using NumPy:

    die = np.random.randint(1, 7)

Possible results:

    1
    2
    3
    4
    5
    6

Why `7`?

Because the upper bound is excluded.

Therefore:

    np.random.randint(1, 7)

means:

    1 <= result < 7

so the possible values are `1` through `6`.

---

# 🏗️ Building Toward the Empire State Building Simulation

The complete simulation will eventually combine:

- `np.random.randint()` → simulate die rolls
- `if` / `elif` / `else` → decide how the roll changes the position
- `while` / `for` loops → repeat the game
- Lists / NumPy arrays → store simulation results
- Random probabilities → simulate falling
- Repeated simulations → estimate the chance of reaching step `60`

This is where the concepts from the course start working together.

---

# 🧠 Example Logic for the Die

The basic movement rules can be expressed using conditional statements:

    if dice == 1 or dice == 2:
        # move down

    elif dice == 3 or dice == 4 or dice == 5:
        # move up

    else:
        # roll again and move up by the new value

Later, a random event will determine whether you fall back to step `0`.

---

# 🔬 Hacker Statistics

The simulation approach works like this:

    Simulate the game
           ↓
    Record the outcome
           ↓
    Repeat many times
           ↓
    Count how often step 60 is reached
           ↓
    Estimate the probability

For example, if a simulation is run `10,000` times and `420` simulations reach step `60`, the estimated probability would be:

    420 / 10000 = 0.042

or:

    4.2%

The actual Empire State Building exercise will build this simulation step by step.

---

# 🔑 Key Takeaways

- NumPy's random functionality is available through:

      np.random

- `np.random.rand()` generates random floating-point numbers between `0` and `1`.
- `np.random.randint(low, high)` generates random integers from `low` **up to but not including** `high`.
- To simulate a six-sided die:

      np.random.randint(1, 7)

- A random seed can be set with:

      np.random.seed(123)

- Setting the same seed produces the same pseudo-random sequence.
- Reproducibility is important in simulations and data analysis.
- Random numbers can be combined with `if`, `elif`, and `else` to simulate real-world events.
- Repeated simulation can be used to estimate probabilities. This approach is known as **Hacker Statistics**.

### 📚 Core Patterns

**Random floating-point number:**

    np.random.rand()

**Set random seed:**

    np.random.seed(123)

**Random integer from 0 or 1:**

    np.random.randint(0, 2)

**Simulate a six-sided die:**

    np.random.randint(1, 7)

**Simple coin toss:**

    coin = np.random.randint(0, 2)

    if coin == 0:
        print("heads")
    else:
        print("tails")

> 🎯 **Core idea:** Random-number generation lets you simulate uncertain events, while repeated simulations let you estimate probabilities using Hacker Statistics.
