# 🪟 SQL Window Functions: Frames
## 📌 Overview
- **Frames** define which rows a window function considers when performing calculations.
- They provide additional control over window functions alongside `PARTITION BY` and `ORDER BY`.
- A frame determines the **starting and ending rows** included in a window function's calculation.
## 1. 🎯 Understanding Frames
- Frames change the behavior of window functions by restricting or extending the rows they can access.
- **Default frame behavior:**
  - Starts at the beginning of the table or partition.
  - Ends at the current row.
  - This means window functions generally consider all preceding rows up to the current row.
- **Example: `LAST_VALUE()`**
  - Without an extended frame, `LAST_VALUE()` returns the current row's value because the default frame ends at the current row.
  - To retrieve the actual last value in the entire partition, extend the frame using:
    - `RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`
## 2. 🛠️ Defining a Frame Using ROWS BETWEEN
- A frame definition starts with either `ROWS BETWEEN` or `RANGE BETWEEN`.
- Every frame has two boundaries:
  - **Starting boundary:** Determines where the frame begins.
  - **Ending boundary:** Determines where the frame stops.
- **Three main boundary options:**
  - `n PRECEDING` → Refers to n rows before the current row.
  - `CURRENT ROW` → Refers to the current row.
  - `n FOLLOWING` → Refers to n rows after the current row.
- **Examples:**
  - `ROWS BETWEEN 3 PRECEDING AND CURRENT ROW`
    - Includes 3 previous rows and the current row (4 rows total).
  - `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING`
    - Includes 1 previous row, the current row, and 1 following row (3 rows total).
  - `ROWS BETWEEN 5 PRECEDING AND 1 PRECEDING`
    - Includes 5 previous rows, excluding the current row (5 rows total).
## 3. 📊 Understanding MAX() with Frames
- **Scenario:** Analyzing the number of gold medals earned by Russia across different Olympic Games.
- **Without an explicitly defined frame:**
  - `MAX()` considers all values from the beginning of the partition up to the current row.
  - It calculates the highest medal count recorded so far.
  - Once the maximum reaches 66, subsequent rows retain 66 unless a higher value appears.
- **With a defined frame:**
  - `ROWS BETWEEN 1 PRECEDING AND CURRENT ROW`
  - Considers only the previous row and the current row.
  - Older rows are excluded from the calculation.
  - Example: In 2008, the maximum is 47 instead of 66 because the 2000 Olympics are outside the frame.
## 4. 🔮 Looking Forward with FOLLOWING
- Frames can also include future rows, not just previous rows.
- **Example:**
  - `ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING`
  - Includes the current row and the next row.
  - `MAX()` compares the values of these two rows.
  - For the last row, only the current row is considered because no following row exists.
## 5. 💻 SQL Syntax and Examples
- **Basic frame syntax:**
  ```sql
  ROWS BETWEEN start_boundary AND end_boundary
  ```
- **Example 1: Previous 3 rows and current row**
  ```sql
  ROWS BETWEEN 3 PRECEDING AND CURRENT ROW
  ```
- **Example 2: Previous, current, and next row**
  ```sql
  ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
  ```
- **Example 3: Current and next row**
  ```sql
  ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING
  ```
- **Example 4: Entire partition**
  ```sql
  RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
  ```
## 6. 🧠 Key Takeaways
- Frames control which rows are included in a window function's calculation.
- `ROWS BETWEEN` defines frame boundaries based on physical row positions.
- `PRECEDING` looks backward, while `FOLLOWING` looks forward.
- `CURRENT ROW` includes the row currently being evaluated.
- Without an explicit frame, the default commonly ends at the current row.
- Defining a frame is useful for:
  - Calculating moving averages.
  - Comparing current and previous records.
  - Analyzing rolling maximums and minimums.
  - Computing cumulative statistics.
  - Retrieving values from other rows within a partition.
- **Remember:** A window function determines *what calculation to perform*, while a frame determines *which rows to use as input*.
## 7. 📝 Practice Reminder
- Practice defining frames using `ROWS BETWEEN`.
- Experiment with `PRECEDING`, `CURRENT ROW`, and `FOLLOWING`.
- Compare window function results with and without explicitly defined frames.
- Next topic: Understanding the difference between `ROWS` and `RANGE`.
