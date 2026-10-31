# SQL Window Functions: Paging with NTILE()

## 1. Introduction to Paging

The third common application of SQL window functions is **paging**.

Paging is the process of dividing a dataset into smaller, approximately equal-sized groups or pages.

It is commonly used in:
- **APIs and web applications:** Dividing large amounts of data into smaller pages so users do not have to retrieve everything at once.
- **Performance analysis:** Dividing records into groups to identify top-performing, average-performing, and low-performing entities.
- **Statistical analysis:** Splitting observations into thirds, quartiles, or other groups for comparison.

SQL provides the `NTILE()` window function to perform this operation.

## 2. Understanding NTILE()

`NTILE(n)` divides an ordered result set into `n` approximately equal-sized groups or buckets.

**Syntax:**

```sql
NTILE(n) OVER (
    ORDER BY column_name
)
```

Where:
- `NTILE(n)` specifies the number of groups or pages.
- `ORDER BY` determines how the records are arranged before they are distributed.
- The resulting column contains the assigned group number, from 1 to n.

For example:

```sql
NTILE(4) OVER (
    ORDER BY Medals DESC
) AS Quartile
```

This divides the records into four approximately equal-sized groups based on medal counts, from highest to lowest.

## 3. Paging Example: Dividing Disciplines into 15 Pages

Suppose we have 67 unique Olympic disciplines and want to divide them into 15 pages.

Because 67 cannot be divided evenly by 15, some pages will contain five rows while others will contain four.

### SQL Example

```sql
WITH Disciplines AS (
    SELECT DISTINCT
        Discipline
    FROM Summer_Medals
)

SELECT
    Discipline,
    NTILE(15) OVER (
        ORDER BY Discipline ASC
    ) AS Page
FROM Disciplines
ORDER BY Page ASC, Discipline ASC;
```

### Explanation

**Step 1: Create the CTE**

```sql
WITH Disciplines AS (
    SELECT DISTINCT
        Discipline
    FROM Summer_Medals
)
```

This retrieves all unique Olympic disciplines from the dataset.

**Step 2: Apply NTILE()**

```sql
NTILE(15) OVER (
    ORDER BY Discipline ASC
) AS Page
```

- `NTILE(15)` divides the records into 15 approximately equal-sized groups.
- `ORDER BY Discipline ASC` arranges the disciplines alphabetically before assigning them to pages.
- `AS Page` names the resulting column.

### Understanding the Distribution

With 67 records divided into 15 pages:

- 7 pages will contain 5 records each.
- 8 pages will contain 4 records each.

| Page | Number of Records |
|---|---:|
| 1 | 5 |
| 2 | 5 |
| 3 | 5 |
| 4 | 5 |
| 5 | 5 |
| 6 | 5 |
| 7 | 5 |
| 8–15 | 4 each |
| **Total** | **67** |

The larger groups are assigned first when the number of rows cannot be divided evenly.

## 4. Using NTILE() to Identify Top, Middle, and Bottom Thirds

Another useful application of `NTILE()` is dividing records into performance categories.

For example, suppose we want to classify countries according to the total number of medals they earned in each Olympic Games.

We can divide the countries into three groups:

1. **Top third:** Countries with the highest medal counts.
2. **Middle third:** Countries with moderate medal counts.
3. **Bottom third:** Countries with the lowest medal counts.

### SQL Example

```sql
WITH Country_Medals AS (
    SELECT
        Year,
        Country,
        COUNT(*) AS Medals
    FROM Summer_Medals
    GROUP BY Year, Country
)

SELECT
    Year,
    Country,
    Medals,
    NTILE(3) OVER (
        PARTITION BY Year
        ORDER BY Medals DESC
    ) AS Third
FROM Country_Medals
ORDER BY Year ASC, Third ASC;
```

### Explanation

**Step 1: Create the CTE**

```sql
WITH Country_Medals AS (
    SELECT
        Year,
        Country,
        COUNT(*) AS Medals
    FROM Summer_Medals
    GROUP BY Year, Country
)
```

This calculates the total number of medals earned by each country in each Olympic Games.

- `Year` identifies the Olympic Games.
- `Country` identifies the participating country.
- `COUNT(*) AS Medals` counts the medal records.
- `GROUP BY Year, Country` calculates medal totals for each country in each year.

**Step 2: Apply NTILE(3)**

```sql
NTILE(3) OVER (
    PARTITION BY Year
    ORDER BY Medals DESC
) AS Third
```

- `NTILE(3)` divides the records into three approximately equal-sized groups.
- `PARTITION BY Year` ensures that countries are divided into thirds separately for each Olympic Games.
- `ORDER BY Medals DESC` places countries with the highest medal counts first.
- `AS Third` names the resulting classification column.

The resulting values represent:

| Third | Classification | Meaning |
|---:|---|---|
| 1 | Top Third | Countries with the highest medal counts |
| 2 | Middle Third | Countries with moderate medal counts |
| 3 | Bottom Third | Countries with the lowest medal counts |

**Important:** `PARTITION BY Year` is included so that countries from different Olympic Games are not ranked or divided into the same groups.

## 5. Calculating the Average Medal Count per Third

After assigning countries to their respective thirds, we can calculate the average number of medals earned by countries in each group.

For example, the top third may have an average medal count of nearly 600, while the middle and bottom thirds have much lower averages.

### SQL Example

```sql
WITH Country_Medals AS (
    SELECT
        Country,
        COUNT(*) AS Medals
    FROM Summer_Medals
    GROUP BY Country
),

Country_Thirds AS (
    SELECT
        Country,
        Medals,
        NTILE(3) OVER (
            ORDER BY Medals DESC
        ) AS Third
    FROM Country_Medals
)

SELECT
    Third,
    AVG(Medals) AS Average_Medals
FROM Country_Thirds
GROUP BY Third
ORDER BY Third ASC;
```

### Explanation

**Step 1: Calculate total medals per country**

The first CTE, `Country_Medals`, calculates the overall medal count for each country across the dataset.

**Step 2: Assign countries to thirds**

The second CTE, `Country_Thirds`, uses `NTILE(3)` to divide countries into three groups based on their medal counts.

**Step 3: Calculate the average**

```sql
SELECT
    Third,
    AVG(Medals) AS Average_Medals
FROM Country_Thirds
GROUP BY Third
ORDER BY Third ASC;
```

- `AVG(Medals)` calculates the average medal count for each third.
- `GROUP BY Third` groups countries according to their assigned classification.
- `ORDER BY Third ASC` displays the top, middle, and bottom thirds in sequence.

## 6. Understanding NTILE() with Other Window Functions

The three ranking and paging concepts covered in this chapter serve different purposes:

| Function | Purpose | Example |
|---|---|---|
| `ROW_NUMBER()` | Assigns unique sequential numbers | Numbering records |
| `RANK()` | Assigns rankings with gaps after ties | Competition rankings |
| `DENSE_RANK()` | Assigns rankings without gaps after ties | Ranking tied athletes |
| `NTILE(n)` | Divides records into approximately equal groups | Paging and performance classification |

### NTILE() vs. RANK()

It is important to understand that `NTILE()` is not the same as a ranking function.

- `RANK()` and `DENSE_RANK()` assign positions based on values and preserve ties.
- `NTILE()` distributes rows into a specified number of groups based on their ordered positions. It does not guarantee that records with identical values will be assigned to the same group.

For example, two countries with identical medal counts may end up in different thirds if they fall on opposite sides of a group boundary.

## 7. Key Takeaways

- Paging divides a dataset into smaller, approximately equal-sized groups.
- `NTILE(n)` specifies how many groups to create.
- `ORDER BY` determines the sequence in which records are distributed.
- `PARTITION BY` allows paging to happen independently within different groups.
- `NTILE(3)` creates three groups, while `NTILE(4)` creates four groups.
- `NTILE()` is useful for pagination, performance classification, and dividing datasets into thirds or quartiles.
- When the total number of records cannot be divided evenly, some groups will contain one more record than others.

**Remember:** `NTILE()` is useful when you want to divide an ordered dataset into approximately equal-sized groups rather than assign a unique ranking to every record.
