# Project 1: Analyzing Mental Health

## Background

Does going to university in a different country affect your mental health?

A Japanese international university surveyed its students in 2018 and published a study the following year that was approved by several ethical and regulatory boards.

The study found that international students have a higher risk of mental health difficulties than the general population, and that **social connectedness** (belonging to a social group) and **acculturative stress** (stress associated with joining a new culture) are predictive of depression.

Explore the `students` data using PostgreSQL to find out if you would come to a similar conclusion for international students and see if the length of stay is a contributing factor.

## Data Description

| Field Name | Description |
|---|---|
| `inter_dom` | Types of students (international or domestic) |
| `japanese_cate` | Japanese language proficiency |
| `english_cate` | English language proficiency |
| `academic` | Current academic level (undergraduate or graduate) |
| `age` | Current age of student |
| `stay` | Current length of stay in years |
| `todep` | Total score of depression (PHQ-9 test) |
| `tosc` | Total score of social connectedness (SCS test) |
| `toas` | Total score of acculturative stress (ASISS test) |

## Task

Explore and analyze the `students` data to see how the length of stay (`stay`) impacts the average mental health diagnostic scores of the **international** students present in the study.

### Requirements

- Return a table with **nine rows** and **five columns**.
- The five columns should be aliased as:
  1. `stay`
  2. `count_int`
  3. `average_phq`
  4. `average_scs`
  5. `average_as`
- The average columns should contain the average of:
  - `todep` (PHQ-9 test)
  - `tosc` (SCS test)
  - `toas` (ASISS test)
- Round the average columns to **two decimal places**.
- The `count_int` column should be the number of international students for each length of stay.
- Sort the results by `stay` in **descending order**.
- Use only **international students** where `inter_dom = 'Inter'`.

## Source CSV

[Source CSV: project_1_analyzing_mental_health.csv](project_1_analyzing_mental_health.csv)

## PostgreSQL Solution

    SELECT
        stay,
        COUNT(inter_dom) AS count_int,
        ROUND(AVG(todep), 2) AS average_phq,
        ROUND(AVG(tosc), 2) AS average_scs,
        ROUND(AVG(toas), 2) AS average_as
    FROM students
    WHERE inter_dom = 'Inter'
    GROUP BY stay
    ORDER BY stay DESC
    LIMIT 9;

## Solution Breakdown

| SQL Part | Purpose |
|---|---|
| `SELECT stay` | Returns the length of stay. |
| `COUNT(inter_dom) AS count_int` | Counts international students for each stay length. |
| `ROUND(AVG(todep), 2) AS average_phq` | Calculates average PHQ-9 depression score, rounded to 2 decimals. |
| `ROUND(AVG(tosc), 2) AS average_scs` | Calculates average social connectedness score, rounded to 2 decimals. |
| `ROUND(AVG(toas), 2) AS average_as` | Calculates average acculturative stress score, rounded to 2 decimals. |
| `FROM students` | Uses the `students` table. |
| `WHERE inter_dom = 'Inter'` | Filters to international students only. |
| `GROUP BY stay` | Groups students by length of stay. |
| `ORDER BY stay DESC` | Sorts stay lengths from longest to shortest. |
| `LIMIT 9` | Returns nine rows. |
