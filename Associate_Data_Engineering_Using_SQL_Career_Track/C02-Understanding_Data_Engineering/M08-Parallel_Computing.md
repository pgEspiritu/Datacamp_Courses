# Parallel Computing

## What Is Parallel Computing?

**Parallel computing**, also called **parallel processing**, is a method of processing data by splitting a large task into smaller subtasks and executing them simultaneously across multiple computers or processing units.

> Parallel computing forms the basis of many modern data processing tools.

## Why Parallel Computing Is Important

Parallel computing is especially useful for **big data** because of:

- **Processing power**
- **Memory requirements**

Instead of requiring one computer to process the entire dataset, the workload can be divided among several computers.

### Basic Concept

**Large Task → Smaller Subtasks → Multiple Computers → Combined Result**

## Example: Folding T-Shirts

Suppose a shop needs to fold **1,000 t-shirts**.

- A senior employee can fold **100 shirts in 15 minutes**.
- A junior employee can fold **100 shirts in 30 minutes**.

### Sequential Processing

If only one employee can work at a time, the fastest employee is the senior employee.

For 1,000 shirts:

**1,000 ÷ 100 = 10 batches**

**10 × 15 minutes = 150 minutes = 2 hours 30 minutes**

### Parallel Processing

Instead, divide the 1,000 shirts into **4 piles of 250 shirts** and assign one pile to each junior employee.

Each junior employee folds 250 shirts in:

**250 ÷ 100 × 30 minutes = 75 minutes**

Therefore, four junior employees working simultaneously can finish in approximately:

**75 minutes = 1 hour 15 minutes**

This is faster than one senior employee working alone.

## Big Data Equivalent

In data processing:

- **Employees** = Processing units / computers
- **T-shirts** = Data
- **Folding** = Data processing task
- **Piles of shirts** = Data partitions
- **Completed piles** = Processed data subsets
- **Combining piles** = Combining processing results

### Parallel Processing Flow

**Large Dataset → Partition Data → Distribute Across Computers → Process in Parallel → Combine Results**

## Benefits of Parallel Computing

### 1. Increased Processing Power

Multiple computers can process different parts of the workload simultaneously.

This can significantly reduce the time required for large processing tasks.

### 2. Reduced Memory Requirement per Computer

A large dataset does not necessarily need to fit entirely into one computer's memory.

Instead:

**Large Dataset → Smaller Partitions → Different Computers**

Each computer only needs to load its assigned subset into memory.

This reduces the **memory footprint per computer**.

### 3. Enables Large-Scale Data Processing

Parallel computing makes it possible to process datasets that may be too large or computationally expensive for a single machine.

## Disadvantages of Parallel Computing

Parallel processing introduces additional overhead.

### 1. Data Movement Cost

Moving data between computers requires:

- Network resources
- Time
- Processing overhead

### 2. Communication Between Processes

Subtasks need to communicate with one another.

The system may need to:

- Split the original task.
- Distribute subtasks.
- Coordinate processing.
- Merge the results.

This communication introduces additional time.

### 3. Task Splitting and Result Merging

The overhead of dividing a task and combining the results may reduce or eliminate the performance benefit if the task is too small.

> Parallel computing is not automatically faster. The performance gain must be greater than the overhead of partitioning, communication, data movement, and combining results.

## T-Shirt Example: Parallel Overhead

In the t-shirt example:

- Separating the shirts into four equal piles takes **10 minutes**.
- Collecting the four piles after folding takes **5 minutes**.
- Folding itself takes **1 hour 15 minutes**.

Total:

**10 + 75 + 5 = 90 minutes**

So the actual process takes:

**1 hour 30 minutes**

instead of the theoretical **1 hour 15 minutes**.

This demonstrates the **overhead of parallel processing**.

## When Parallel Computing Is Useful

Parallel computing is most beneficial when:

- The dataset is very large.
- The task can be divided into independent subtasks.
- Multiple processing units are available.
- The processing time saved is greater than the communication and coordination overhead.

It may not be worthwhile when:

- The task is very small.
- Subtasks cannot be effectively separated.
- Data movement is expensive.
- Communication overhead is significant.
- The performance gains are minimal.

## Parallel Computing at Spotflix

Spotflix uses parallel computing to convert songs from **lossless formats to `.ogg`**.

The processing task involves converting many songs.

Instead of loading all new songs onto one computer:

**New Songs → Partition Songs → Multiple Computers → Convert to `.ogg` → Combined Output**

### Benefits at Spotflix

- Reduces the amount of data that must be loaded into one computer's memory.
- Provides additional processing power.
- Allows multiple song conversions to run simultaneously.
- Makes large-scale song conversion more efficient.

## Parallel Computing vs. Sequential Processing

| Feature | Sequential Processing | Parallel Processing |
|---|---|---|
| **Processing units** | Usually one | Multiple |
| **Task execution** | One task/subtask at a time | Multiple subtasks simultaneously |
| **Memory** | One system may need the entire dataset | Data can be partitioned across systems |
| **Processing power** | Limited to one system | Combined power of multiple systems |
| **Data movement** | Lower | Higher |
| **Communication overhead** | Low | Higher |
| **Best for** | Smaller/simple tasks | Large and divisible workloads |

## Key Terms

### Processing Unit

A computer or computational resource that performs part of a processing task.

### Partition

A smaller subset of a larger dataset or workload.

### Parallel Processing

Processing multiple subtasks at the same time using multiple processing units.

### Memory Footprint

The amount of memory required by a particular process or workload.

### Overhead

The additional time and resources required to coordinate a parallel task, including:

- Data movement
- Communication
- Task splitting
- Result merging

## Exam / Interview Key Points

- **Parallel computing = Parallel processing**.
- Parallel computing divides a large task into **smaller subtasks**.
- These subtasks are distributed across **multiple computers or processing units**.
- Parallel computing is fundamental to many modern big data processing systems.
- It provides additional **processing power**.
- It can reduce the **memory requirement per computer** by partitioning the data.
- Each computer can process a subset of the overall dataset.
- Parallel computing introduces **overhead**.
- Data movement between computers incurs a cost.
- Processes must communicate when splitting tasks and combining results.
- Splitting and merging tasks also require additional time.
- Parallel computing is most beneficial when the performance gain is greater than the overhead.
- **Data partitioning** allows large datasets to be distributed across multiple systems.
- Spotflix uses parallel computing to convert songs from **lossless formats to `.ogg`**.
- Parallel processing prevents all new songs from having to be loaded into one computer.
- More processing units can provide additional computing power.

## Quick Memory Aid

**Parallel Computing = Split → Distribute → Process → Combine**

**Benefit:**

**More computers → More processing power + Smaller memory load per computer**

**Cost:**

**Data movement + Communication + Splitting + Merging = Overhead**

## Most Important Concept

> **Parallel computing processes large workloads by dividing them into smaller subtasks and executing those subtasks simultaneously across multiple processing units. It improves processing power and reduces memory requirements per computer, but introduces overhead from data movement, communication, task splitting, and result merging.**
