# 📊 Distribution of Random Walks

## 📌 Overview

This final lesson brings together the random walk concepts from the chapter.

The main question is:

> **What is the chance that you will reach 60 steps high in the Empire State Building game?**

A single random walk produces one final position. But if we simulate the same random walk **thousands of times**, we get thousands of final positions.

Those final positions form a **distribution**.

Once we have this distribution, we can estimate probabilities.

---

# 🚶 From Random Walk to Distribution

Suppose you throw a die `100` times and update your position according to the game rules.

One simulation might finish at:

    42

Another might finish at:

    57

Another might finish at:

    63

Another might finish at:

    48

Each simulation can end at a different step.

If we repeat the simulation thousands of times, we get a collection like:

    [42, 57, 63, 48, 51, 60, 44, ...]

This collection of final positions is a **distribution of final steps**.

---

# 🎯 Why Simulate Many Random Walks?

The original question is:

> What is the probability of reaching at least step `60`?

A single simulation cannot answer this reliably.

Instead:

1. Simulate the random walk.
2. Record its final position.
3. Repeat the simulation many times.
4. Examine the distribution of final positions.
5. Calculate how often the final position reaches the target.

The more simulations we perform, the better our estimate can become.

---

# 🪙 Example: Total Tails After 10 Coin Tosses

Before applying this idea to the Empire State Building, consider a simpler example.

We toss a coin `10` times.

Using:

    0 → Heads
    1 → Tails

we can track the cumulative number of tails.

Start with:

    tails = [0]

Then repeat `10` times:

    coin = np.random.randint(0, 2)
    tails.append(tails[-1] + coin)

The final value in `tails` represents the total number of tails after `10` tosses.

---

# 🔢 One Game vs Many Games

A single game of `10` tosses produces one final number between:

    0 and 10

For example:

    tails = [0, 1, 1, 2, 3, 3, 4, 5, 5, 6, 6]

The final value is:

    6

This means there were `6` tails in the `10` tosses.

But we want to know how the result behaves when we play the game repeatedly.

---

# 🔄 Simulating 100 Games

Create an empty list:

    final_tails = []

This list will store the **final number of tails from every game**.

Then simulate the entire 10-toss game `100` times.

### Example

    import numpy as np

    np.random.seed(123)

    final_tails = []

    for i in range(100):
        tails = [0]

        for j in range(10):
            coin = np.random.randint(0, 2)
            tails.append(tails[-1] + coin)

        final_tails.append(tails[-1])

    print(final_tails)

---

# 🧠 Understanding the Nested Loops

There are two loops:

### Outer Loop

    for i in range(100):

Runs the entire game **100 times**.

### Inner Loop

    for j in range(10):

Runs the coin toss **10 times per game**.

The structure is:

    Repeat the game 100 times:
        Start a new game
        Toss the coin 10 times
        Record the final number of tails

---

# 📋 What Goes into `final_tails`

Suppose the first few games finish with:

    4 tails
    7 tails
    5 tails
    6 tails
    3 tails

Then:

    final_tails = [4, 7, 5, 6, 3, ...]

Each element represents the final result of one complete game.

After `100` simulations:

    len(final_tails)

is:

    100

---

# 📊 From Final Results to a Distribution

The values in `final_tails` form a distribution.

Possible values are:

    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10

Each number represents how many tails occurred in one game of `10` tosses.

---

# 📈 Visualizing the Distribution with a Histogram

A histogram is useful for visualizing the distribution.

First import Matplotlib:

    import matplotlib.pyplot as plt

Then:

    plt.hist(final_tails, bins=10)
    plt.show()

The histogram shows how frequently each final number of tails occurred.

---

# 🧱 Why Use `bins=10`?

The possible number of tails ranges from:

    0 to 10

Using:

    bins=10

divides the results into histogram bins so the distribution can be visualized.

The exact appearance depends on the data and the number of simulations.

---

# 📉 100 Simulations

With:

    for i in range(100):

the histogram may look somewhat irregular.

There are only `100` observations, so the distribution is based on a relatively small sample.

You can still see the general pattern, but it may not be very smooth.

---

# 📈 1,000 Simulations

Change:

    range(100)

to:

    range(1000)

Now the simulation is performed `1,000` times.

The histogram generally becomes smoother because it is based on more observations.

---

# 📈 10,000 Simulations

Increase the number again:

    range(10000)

Now the distribution becomes much more stable.

With enough simulations, the simulated distribution begins to approach the **theoretical distribution**.

---

# 🧠 Simulated vs Theoretical Distribution

## Simulated Distribution

Produced by repeatedly running the random experiment.

For example:

    10000 simulated games
        ↓
    10000 final results
        ↓
    Histogram

## Theoretical Distribution

The distribution obtained through mathematical analysis and probability calculations.

The simulated results tend to **converge toward** the theoretical distribution as the number of simulations increases.

---

# 🔬 Law of Large Numbers — Intuition

The more times you repeat a random experiment, the more stable the observed distribution tends to become.

For example:

    100 simulations
        ↓
    More variation

    1,000 simulations
        ↓
    Smoother distribution

    10,000 simulations
        ↓
    Even closer to the theoretical pattern

This is one reason why simulation is useful for estimating probabilities.

---

# 📊 Example: 10,000 Coin-Toss Games

Suppose we simulate:

    10000

games of `10` coin tosses.

If approximately `2500` games finish with exactly `5` tails, then:

    2500 / 10000

equals:

    0.25

or:

    25%

So approximately `25%` of the simulated games resulted in exactly `5` tails.

> 💡 The exact percentage can vary depending on the simulation and random seed.

---

# 🎯 Applying This to the Empire State Building

The same technique can be used for the Empire State Building random walk.

Instead of simulating:

    10 coin tosses

we simulate:

    100 dice rolls

and record the final position.

Then repeat the entire random walk many times.

The process becomes:

    Simulate one 100-step random walk
                ↓
        Record final step
                ↓
            Repeat many times
                ↓
      Collect final positions
                ↓
       Build a distribution
                ↓
     Estimate probability of
        reaching step 60

---

# 🏢 Empire State Building Distribution

For each simulation:

    random_walk = [0]

Then perform the dice-based random walk.

After `100` dice rolls:

    random_walk[-1]

is the final position.

Store it in a list such as:

    final_steps

After many simulations:

    final_steps = [
        final_position_1,
        final_position_2,
        final_position_3,
        ...
    ]

This gives us the distribution of final positions.

---

# 🔄 General Simulation Pattern

A common structure is:

    final_results = []

    for i in range(number_of_simulations):
        # simulate one complete random process
        # ...
        final_results.append(final_result)

This pattern is extremely useful for **Monte Carlo simulation** and other forms of computational probability.

---

# 🧠 Important Concepts

## Distribution

A collection of possible outcomes and how frequently they occur.

## Simulation

Repeatedly running a random process to study its behavior.

## Histogram

A graph that shows the distribution of numerical values by counting how many observations fall into different ranges.

## Theoretical Distribution

A mathematically derived distribution.

## Simulated Distribution

A distribution generated from repeated random experiments.

---

# 📚 Complete Coin-Toss Simulation Example

    import numpy as np
    import matplotlib.pyplot as plt

    np.random.seed(123)

    final_tails = []

    for i in range(10000):
        tails = [0]

        for j in range(10):
            coin = np.random.randint(0, 2)
            tails.append(tails[-1] + coin)

        final_tails.append(tails[-1])

    plt.hist(final_tails, bins=10)
    plt.show()

---

# 🔍 Code Breakdown

### Start the Results List

    final_tails = []

Stores the final result from every game.

### Simulate 10,000 Games

    for i in range(10000):

Runs the entire experiment 10,000 times.

### Start Each Game at Zero Tails

    tails = [0]

### Toss the Coin 10 Times

    for j in range(10):

### Generate a Random Toss

    coin = np.random.randint(0, 2)

### Update the Running Total

    tails.append(tails[-1] + coin)

### Record the Final Result

    final_tails.append(tails[-1])

### Visualize the Distribution

    plt.hist(final_tails, bins=10)
    plt.show()

---

# 🧠 Why Store Only `tails[-1]`?

The `tails` list tracks the entire random walk within one game:

    [0, 1, 1, 2, 2, 3, 4, 4, 5, 5, 6]

But for the distribution, we only need the **final number of tails**:

    6

Therefore:

    final_tails.append(tails[-1])

stores only the final outcome of each game.

---

# 🔑 Key Takeaways

- A single random walk produces one final result.
- Repeating the random walk thousands of times produces a **distribution of final results**.
- A histogram is a useful way to visualize this distribution.
- More simulations generally produce a smoother and more stable estimate.
- Simulated distributions tend to approach theoretical distributions as the number of simulations increases.
- The final value of a random walk can be stored in a list for later analysis.
- Repeated simulation is a practical way to estimate probabilities.
- For the Empire State Building problem, the distribution of final steps can be used to estimate the chance of reaching `60` steps.

### 📚 Core Pattern

    final_results = []

    for i in range(number_of_simulations):
        # Build one random walk
        random_walk = [0]

        for j in range(number_of_steps):
            # Generate random step
            # Update random_walk
            ...

        final_results.append(random_walk[-1])

    plt.hist(final_results)
    plt.show()

> 🎯 **Core idea:** Simulate the entire random process many times, record the final outcome of each run, and use the resulting distribution to estimate probabilities.
