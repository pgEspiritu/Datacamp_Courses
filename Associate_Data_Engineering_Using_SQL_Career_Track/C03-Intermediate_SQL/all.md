# SQL Quick Reference

| Topic Title | Keyword / Syntax | Function / Meaning | Sample Syntax |
|---|---|---|---|
| SQL | `SQL` | Structured Query Language; used to communicate with and query databases. | `SELECT name FROM patrons;` |
| Query | Query | A request for data from a database. | `SELECT title FROM films;` |
| Select fields | `SELECT` | Specifies which fields/columns to retrieve. | `SELECT name FROM patrons;` |
| Select all fields | `*` | Selects all fields in a table. | `SELECT * FROM patrons;` |
| Specify table | `FROM` | Specifies the table where the fields are located. | `SELECT name FROM patrons;` |
| End query | `;` | Indicates the end of a query; considered best practice. | `SELECT name FROM patrons;` |
| Alias | `AS` | Renames a field or table reference without changing the underlying database object. | `SELECT name AS first_name FROM employees;` |
| Table alias | `AS` | Gives a table a temporary name, useful especially for joins and self joins. | `FROM prime_ministers AS p1` |
| Unique values | `DISTINCT` | Returns only unique values. | `SELECT DISTINCT year_hired FROM employees;` |
| Unique combinations | `DISTINCT` with multiple fields | Returns unique combinations of multiple field values. | `SELECT DISTINCT dept_id, year_hired FROM employees;` |
| Count values | `COUNT(field)` | Counts non-NULL values in a field. | `SELECT COUNT(birthdate) FROM people;` |
| Count records | `COUNT(*)` | Counts the total number of records. | `SELECT COUNT(*) FROM people;` |
| Count unique values | `COUNT(DISTINCT field)` | Counts unique values in a field. | `SELECT COUNT(DISTINCT birthdate) FROM people;` |
| Filter records | `WHERE` | Filters records based on a condition. | `SELECT title FROM films WHERE release_year = 2000;` |
| Greater than | `>` | Filters values greater than a specified value. | `WHERE release_year > 1960` |
| Less than | `<` | Filters values less than a specified value. | `WHERE release_year < 1960` |
| Equal to | `=` | Filters values equal to a specified value. | `WHERE release_year = 1960` |
| Greater than or equal | `>=` | Filters values greater than or equal to a specified value. | `WHERE release_year >= 1960` |
| Less than or equal | `<=` | Filters values less than or equal to a specified value. | `WHERE release_year <= 1960` |
| Not equal | `<>` | Filters values that are not equal. | `WHERE release_year <> 1960` |
| Text filtering | Single quotes `' '` | Encloses string values used in filtering. | `WHERE country = 'Japan'` |
| Multiple criteria | `OR` | At least one condition must be satisfied. | `WHERE release_year = 1994 OR release_year = 2000` |
| Multiple criteria | `AND` | All conditions must be satisfied. | `WHERE release_year >= 1994 AND release_year <= 2000` |
| Range filtering | `BETWEEN ... AND ...` | Filters values within an inclusive range. | `WHERE release_year BETWEEN 1994 AND 2000` |
| Text pattern matching | `LIKE` | Searches for a text pattern. | `WHERE name LIKE 'Ad%'` |
| Exclude text pattern | `NOT LIKE` | Finds records that do not match a text pattern. | `WHERE name NOT LIKE 'A%'` |
| Multiple exact values | `IN` | Matches any value in a specified list. | `WHERE release_year IN (1920, 1930, 1940)` |
| LIKE wildcard | `%` | Matches zero, one, or many characters. | `WHERE name LIKE 'Ad%'` |
| LIKE wildcard | `_` | Matches exactly one character. | `WHERE name LIKE '___'` |
| Starts with | `%` | Matches any characters after the specified text. | `WHERE name LIKE 'Ad%'` |
| Ends with | `%` | Matches any characters before the specified text. | `WHERE name LIKE '%r'` |
| Contains | `%` | Matches any characters before and after the specified text. | `WHERE name LIKE '%ad%'` |
| Specific character position | `_` | Matches exact character positions. | `WHERE name LIKE '__t%'` |
| Missing value | `NULL` | Represents a missing or unknown value. | `WHERE birthdate IS NULL` |
| Find missing values | `IS NULL` | Identifies records containing NULL. | `SELECT * FROM people WHERE birthdate IS NULL;` |
| Find non-missing values | `IS NOT NULL` | Identifies records that do not contain NULL. | `SELECT * FROM people WHERE birthdate IS NOT NULL;` |
| Count missing values | `COUNT(*)` + `IS NULL` | Counts records where a field is NULL. | `SELECT COUNT(*) FROM people WHERE birthdate IS NULL;` |
| Count non-missing values | `COUNT(*)` + `IS NOT NULL` | Counts records where a field is not NULL. | `SELECT COUNT(*) FROM people WHERE birthdate IS NOT NULL;` |
| Average | `AVG()` | Calculates the average of a numerical field. | `SELECT AVG(budget) FROM films;` |
| Sum | `SUM()` | Adds values in a numerical field. | `SELECT SUM(budget) FROM films;` |
| Minimum | `MIN()` | Returns the lowest value; for text, alphabetically first; for dates, earliest. | `SELECT MIN(budget) FROM films;` |
| Maximum | `MAX()` | Returns the highest value; for text, alphabetically last; for dates, latest. | `SELECT MAX(budget) FROM films;` |
| Round numbers | `ROUND()` | Rounds a numerical value to a specified number of decimal places. | `SELECT ROUND(AVG(budget), 2) FROM films;` |
| Round to whole number | `ROUND(number)` | Rounds to a whole number when the second argument is omitted. | `SELECT ROUND(AVG(budget)) FROM films;` |
| Round to decimal places | `ROUND(number, decimal_place)` | Rounds to the specified decimal position. | `SELECT ROUND(AVG(budget), 2) FROM films;` |
| Negative rounding | `ROUND(number, -n)` | Rounds to the left of the decimal point. | `SELECT ROUND(1234567, -5);` |
| Addition | `+` | Adds values. | `SELECT 10 + 5;` |
| Subtraction | `-` | Subtracts values. | `SELECT 10 - 5;` |
| Multiplication | `*` | Multiplies values. | `SELECT 10 * 5;` |
| Division | `/` | Divides values; integer division can return an integer when both operands are integers. | `SELECT 5 / 3;` |
| Decimal division | Decimal values | Using decimal operands provides greater precision in division. | `SELECT 4.0 / 3.0;` |
| Arithmetic grouping | `( )` | Controls arithmetic order and improves clarity. | `SELECT (10 + 5) * 2;` |
| Profit calculation | `gross - budget` | Calculates profit by subtracting budget from gross. | `SELECT gross - budget AS profit FROM films;` |
| Group data | `GROUP BY` | Groups records by one or more fields, usually for aggregation. | `SELECT certification, AVG(duration) FROM films GROUP BY certification;` |
| Group by multiple fields | `GROUP BY field1, field2` | Groups records by combinations of multiple fields. | `SELECT certification, language, COUNT(title) FROM films GROUP BY certification, language;` |
| Filter grouped data | `HAVING` | Filters grouped results, especially aggregate results. | `SELECT release_year, COUNT(title) FROM films GROUP BY release_year HAVING COUNT(title) > 10;` |
| Sort results | `ORDER BY` | Sorts query results by one or more fields. | `SELECT title, budget FROM films ORDER BY budget;` |
| Ascending order | `ASC` | Sorts ascending, such as smallest to largest or A to Z. | `ORDER BY title ASC` |
| Descending order | `DESC` | Sorts descending, such as largest to smallest or Z to A. | `ORDER BY budget DESC` |
| Multiple sorting fields | `ORDER BY field1, field2` | Sorts by the first field and uses later fields as tie-breakers. | `ORDER BY oscar_wins DESC, imdb_score DESC` |
| Different sort directions | `ASC`, `DESC` | Allows different directions for different fields. | `ORDER BY birthdate ASC, name DESC` |
| Limit results | `LIMIT` | Limits the number of returned records. | `SELECT name FROM people LIMIT 10;` |
| SQL Server row limit | `TOP` | SQL Server syntax for limiting returned rows. | `SELECT TOP 2 name FROM employees;` |
| Save query | `CREATE VIEW` | Saves a query as a view. | `CREATE VIEW employee_hire_years AS SELECT DISTINCT year_hired FROM employees;` |
| Define view query | `AS` | Defines the query stored in a view. | `CREATE VIEW employee_hire_years AS SELECT year_hired FROM employees;` |
| Query a view | `SELECT ... FROM view` | Queries a view like a table. | `SELECT * FROM employee_hire_years;` |
| View | `VIEW` | A saved SQL query that acts like a virtual table; it stores the query rather than the data. | `SELECT * FROM employee_hire_years;` |
| Database | Database | Stores and organizes data. | `SELECT * FROM patrons;` |
| Table | Table | Contains records and fields within a database. | `SELECT * FROM patrons;` |
| Record | Row | Represents one individual observation or entity. | `One patron = one record` |
| Field | Column | Contains one piece of information for every record. | `name` |
| Unique identifier | Key / unique identifier | A field that uniquely identifies each record. | `card_num` |
| Relational database | Relational database | Contains related tables that share information. | `patrons`, `books`, `checkouts` |
| Database schema | Schema | Blueprint showing tables, relationships, and field data types. | `patrons` related to `checkouts` |
| String | String | A sequence of characters. | `"Maham"` |
| String data type | `VARCHAR` | Stores character/string values. | `name VARCHAR(255)` |
| Integer data type | `INT` | Stores whole numbers without decimals. | `employee_id INT` |
| Decimal data type | `NUMERIC` | Stores numbers with fractional/decimal values. | `total_fine NUMERIC` |
| Boolean data type | `BOOLEAN` | Stores logical values such as true/false. | `full_time BOOLEAN` |
| Server | Server | A powerful computer that stores information and performs services through network requests. | `Database stored on a server` |
| SQL flavor | SQL flavor | A particular implementation of SQL used by a database system. | `PostgreSQL` |
| PostgreSQL | PostgreSQL | Free and open-source relational database system used in the course. | `SELECT title FROM films LIMIT 2;` |
| SQL Server | SQL Server | Microsoft's relational database system. | `SELECT TOP 2 name FROM employees;` |
| T-SQL | T-SQL | Microsoft's proprietary SQL flavor for SQL Server. | `SELECT TOP 2 name FROM employees;` |
| SQL standard | ISO / ANSI | SQL flavors share standards associated with ISO and ANSI. | Standard SQL |
| Query execution order | `FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT` | Logical execution order for the covered clauses. | `SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... LIMIT ...;` |
| Simplified execution order | `FROM → SELECT → LIMIT` | Earlier simplified logical execution order. | `SELECT name FROM people LIMIT 10;` |
| Filter before selection | `FROM → WHERE → SELECT` | `WHERE` is logically processed before `SELECT`. | `SELECT title FROM films WHERE release_year = 2000;` |
| Group before selection | `GROUP BY → SELECT` | Grouping occurs before the `SELECT` step. | `GROUP BY certification` |
| HAVING before SELECT | `HAVING → SELECT` | Explains why a `SELECT` alias cannot be used in `HAVING` in the lesson. | `HAVING COUNT(title) > 10` |
| ORDER BY after SELECT | `SELECT → ORDER BY` | Allows a `SELECT` alias to be used in `ORDER BY`. | `ORDER BY title_count DESC` |
| SQL error | Misspelled field | Causes an error when a field name is incorrect. | `SELECT nmae FROM people;` |
| SQL error | Missing comma | Common error when separating selected fields. | `SELECT title, country, duration FROM films;` |
| SQL error | Misspelled keyword | Causes a SQL error when a keyword is incorrect. | `SELCT name FROM people;` |
| Error indicator | `^` | Indicates approximately where SQL detected an error. | `^` |
| Debugging | Debugging | Finding and correcting SQL errors by checking spelling, punctuation, fields, and syntax. | Check field names and commas |

## 🔗 JOINS

| Topic Title | Keyword / Syntax | Function / Meaning | Sample Syntax |
|---|---|---|---|
| Join | `JOIN` | Combines data from separate tables. | `SELECT ... FROM table1 INNER JOIN table2 ON table1.id = table2.id;` |
| Inner join | `INNER JOIN` | Returns only records with matching values in both tables. | `FROM presidents AS p INNER JOIN prime_ministers AS pm ON p.country = pm.country` |
| Join condition | `ON` | Specifies the fields/conditions used to match records. | `ON p.country = pm.country` |
| Join using same field name | `USING` | Shortcut when both tables have the same join-field name. | `USING (country)` |
| Qualified field | `table.column` | Identifies a column using its table name/alias; useful when names are duplicated. | `SELECT p.country FROM presidents AS p;` |
| One-to-many relationship | One-to-many | One entity can be related to many records in another table. | `author → many books` |
| One-to-one relationship | One-to-one | One record corresponds to one record. | `one fingerprint set ↔ one record` |
| Many-to-many relationship | Many-to-many | Many records in one table can relate to many records in another. | `languages ↔ countries` |
| Multiple joins | Multiple `JOIN`s | Chains joins to combine more than two tables. | `FROM presidents p INNER JOIN prime_ministers pm ON ... INNER JOIN prime_minister_terms t ON ...` |
| Multiple join keys | `AND` in `ON` | Uses multiple conditions to match records. | `ON a.id = b.id AND a.date = b.date` |
| Left join | `LEFT JOIN` | Returns all records from the left table plus matching records from the right table. | `FROM left_table LEFT JOIN right_table ON left_table.id = right_table.id` |
| Left outer join | `LEFT OUTER JOIN` | Same behavior as `LEFT JOIN`. | `FROM left_table LEFT OUTER JOIN right_table ON ...` |
| Right join | `RIGHT JOIN` | Returns all records from the right table plus matching records from the left table. | `FROM left_table RIGHT JOIN right_table ON ...` |
| Right outer join | `RIGHT OUTER JOIN` | Same behavior as `RIGHT JOIN`. | `FROM left_table RIGHT OUTER JOIN right_table ON ...` |
| Full join | `FULL JOIN` | Returns all records from both tables, whether matched or unmatched. | `FROM table1 FULL JOIN table2 ON table1.country = table2.country` |
| Full outer join | `FULL OUTER JOIN` | Same behavior as `FULL JOIN`. | `FROM table1 FULL OUTER JOIN table2 ON ...` |
| Cross join | `CROSS JOIN` | Creates every possible combination of rows from two tables. | `SELECT * FROM table1 CROSS JOIN table2;` |
| Cartesian product | Cross join result | If table1 has 3 rows and table2 has 3 rows, the result has 9 combinations. | `3 × 3 = 9` |
| Cross join condition | No `ON` / `USING` | `CROSS JOIN` does not require a matching condition. | `FROM table1 CROSS JOIN table2` |
| Cross join filtering | `WHERE` with `CROSS JOIN` | Filters the combinations after creating them. | `FROM prime_ministers pm CROSS JOIN presidents p WHERE pm.continent = 'Asia' AND p.continent = 'South America'` |
| Self join | Self join | Joins a table to itself to compare values within the same table. | `FROM prime_ministers AS p1 INNER JOIN prime_ministers AS p2 ON ...` |
| Self join syntax | No `SELF JOIN` keyword | SQL has no dedicated `SELF JOIN` syntax; use a normal join with aliases. | `prime_ministers AS p1 INNER JOIN prime_ministers AS p2` |
| Self join aliases | `p1`, `p2` | Required to distinguish the two references to the same table. | `FROM prime_ministers AS p1 INNER JOIN prime_ministers AS p2` |
| Self join same continent | `ON p1.continent = p2.continent` | Pairs countries from the same continent. | `ON p1.continent = p2.continent` |
| Exclude self-match | `<>` in `ON` | Prevents a record from being paired with itself. | `AND p1.country <> p2.country` |

## 🔄 SET OPERATIONS

| Topic Title | Keyword / Syntax | Function / Meaning | Sample Syntax |
|---|---|---|---|
| Set operations | `UNION`, `INTERSECT`, `EXCEPT` | SQL operations for combining or comparing result sets. | `SELECT ... FROM table1 UNION SELECT ... FROM table2;` |
| UNION | `UNION` | Returns records from both result sets and removes duplicates. | `SELECT country FROM monarchs UNION SELECT country FROM prime_ministers;` |
| UNION ALL | `UNION ALL` | Returns records from both result sets and keeps duplicates. | `SELECT country FROM monarchs UNION ALL SELECT country FROM prime_ministers;` |
| INTERSECT | `INTERSECT` | Returns only records that exist in both result sets. | `SELECT country FROM prime_ministers INTERSECT SELECT country FROM presidents;` |
| EXCEPT | `EXCEPT` | Returns records from the left result set that are not present in the right result set. | `SELECT country FROM monarchs EXCEPT SELECT country FROM prime_ministers;` |
| Set operation syntax | `SELECT ... OPERATOR SELECT ...` | Performs the selected set operation between two `SELECT` statements. | `SELECT column1 FROM table1 UNION SELECT column1 FROM table2;` |
| Set operation columns | Same number of columns | Both `SELECT` statements must return the same number of columns. | `SELECT country, leader ... UNION SELECT country, leader ...` |
| Set operation data types | Matching data types | Corresponding columns must have matching data types. | `SELECT country, leader ... UNION SELECT country, leader ...` |
| Set operation field names | First `SELECT` names | Result field names come from the first `SELECT`, including its aliases. | `SELECT monarch AS leader ... UNION SELECT prime_minister ...` |
| Set operations vs joins | No `ON` / `USING` | Set operations do not match tables through an `ON` condition. | `SELECT ... FROM table1 UNION SELECT ... FROM table2` |
| Set operations behavior | Stack results | Set operations stack result fields/rows rather than adding columns through a join relationship. | `SELECT country FROM table1 UNION SELECT country FROM table2` |
| UNION duplicate behavior | Duplicate removal | Identical records appearing in both results are returned once. | `UNION` |
| UNION ALL duplicate behavior | Duplicate retention | Identical records appearing in both results remain in the output. | `UNION ALL` |
| INTERSECT matching | All selected fields | For a record to appear, all selected fields must match their corresponding fields. | `SELECT country, leader FROM table1 INTERSECT SELECT country, leader FROM table2` |
| EXCEPT matching | Whole selected record | A left-side record is excluded only when the whole selected record matches the right-side result. | `SELECT id, name FROM left_table EXCEPT SELECT id, name FROM right_table` |

## 🔍 SUBQUERIES

| Topic Title | Keyword / Syntax | Function / Meaning | Sample Syntax |
|---|---|---|---|
| Subquery | Subquery | A SQL query embedded inside another SQL query. | `WHERE country IN (SELECT country FROM states WHERE indep_year < 1800)` |
| Nested query | Query inside query | Allows the result of one query to be used by another query. | `SELECT ... WHERE field IN (SELECT ...);` |
| Additive join | Join | The joins covered earlier add columns to the original left table. | `FROM left_table INNER JOIN right_table ON ...` |
| Semi join | Semi join | Returns records from the first table where a condition is met by values in the second table. | `WHERE country IN (SELECT country FROM states ...)` |
| Semi join with `IN` | `IN (subquery)` | Keeps first-table records whose values occur in the subquery result. | `WHERE country IN (SELECT country FROM states WHERE indep_year < 1800)` |
| Anti join | Anti join | Returns records from the first table where a matching value does not exist in the second table. | `WHERE country NOT IN (SELECT country FROM states ...)` |
| Anti join with `NOT IN` | `NOT IN (subquery)` | Keeps first-table records whose values are not in the subquery result. | `WHERE country NOT IN (SELECT country FROM states WHERE indep_year <= 1800)` |
| Subquery in `WHERE` | `WHERE field IN (subquery)` | Uses the subquery result as filter values. | `WHERE country IN (SELECT country FROM states WHERE indep_year < 1800)` |
| WHERE subquery data type | Matching data type | The subquery result must have the same data type as the field being filtered. | `WHERE some_field IN (SELECT some_numeric_field FROM another_table)` |
| WHERE subquery same table | Same-table subquery | A subquery inside `WHERE` can query the same table. | `WHERE field IN (SELECT field FROM some_table ...)` |
| WHERE subquery different table | Different-table subquery | A subquery inside `WHERE` can query another table. | `WHERE country IN (SELECT country FROM states ...)` |
| Subquery in `SELECT` | Subquery inside `SELECT` | Returns a calculated/value result as part of the selected output. | `SELECT continent, (SELECT COUNT(*) FROM monarchs ...) AS monarch_count FROM states;` |
| SELECT subquery count | `COUNT(*)` in subquery | Counts records from the table queried by the subquery. | `(SELECT COUNT(*) FROM monarchs WHERE monarchs.continent = states.continent)` |
| Correlated SELECT subquery | Outer-reference condition | The subquery uses a field from the outer query to calculate a value for each outer record/group. | `WHERE monarchs.continent = states.continent` |
| Alias SELECT subquery | `AS monarch_count` | A subquery inside `SELECT` requires an alias for its result. | `(SELECT COUNT(*) ...) AS monarch_count` |
| Subquery in `FROM` | Subquery inside `FROM` | Uses a subquery as a temporary table. | `FROM (SELECT continent, MAX(indep_year) AS most_recent FROM states GROUP BY continent) AS sub` |
| FROM subquery alias | `AS sub` | Gives the temporary-table subquery a name that the outer query can reference. | `(...) AS sub` |
| Query temporary table | `sub.field` | Allows the outer query to select fields produced by the subquery. | `SELECT sub.most_recent FROM (...) AS sub` |
| Multiple tables in `FROM` | `FROM table1, table2` | Includes multiple tables in the `FROM` clause; matching can be handled using `WHERE`. | `FROM monarchs AS m, (...) AS sub WHERE m.continent = sub.continent` |
| Duplicate results from multiple tables | Multiple matches | Multiple matching rows can create duplicate records. | `SELECT ... FROM table1, table2 WHERE table1.id = table2.id` |
| Remove duplicates | `DISTINCT` | Removes duplicate result records when multiple matches produce the same output. | `SELECT DISTINCT m.continent, sub.most_recent ...` |
| FROM subquery ordering | `ORDER BY` | Sorts the final result after selecting from the temporary subquery. | `ORDER BY continent` |

# 🔗 JOIN TYPE QUICK COMPARISON

| Join Type | What It Returns | Adds Columns? | Match Required? |
|---|---|---:|---:|
| `INNER JOIN` | Only matching records from both tables | ✅ | ✅ |
| `LEFT JOIN` | All left records + matching right records | ✅ | Right match optional |
| `RIGHT JOIN` | All right records + matching left records | ✅ | Left match optional |
| `FULL JOIN` | All records from both tables | ✅ | Match optional |
| `CROSS JOIN` | Every possible row combination | ✅ | ❌ |
| `SELF JOIN` | A table joined to itself for comparison | ✅ | Depends on join used |
| Semi join | Matching records from first table only | ❌ | ✅ |
| Anti join | Non-matching records from first table only | ❌ | ❌ |

# 🔄 SET OPERATION QUICK COMPARISON

| Operation | Result | Duplicate Handling |
|---|---|---|
| `UNION` | Records from both result sets | Removes duplicates |
| `UNION ALL` | Records from both result sets | Keeps duplicates |
| `INTERSECT` | Records common to both result sets | Common records only |
| `EXCEPT` | Records in left result set but not right result set | Left-only records |

# 🔍 SUBQUERY QUICK COMPARISON

| Subquery Location | Main Purpose | Typical Pattern |
|---|---|---|
| `WHERE` | Filter records | `WHERE field IN (subquery)` |
| `SELECT` | Calculate/return a value | `SELECT (subquery) AS alias` |
| `FROM` | Use subquery as a temporary table | `FROM (subquery) AS alias` |

# 📊 MAIN TABLE AND RESULT TABLE EXAMPLES

## 1. INNER JOIN Example

### Main Tables

**`presidents`**

| country | president |
|---|---|
| Portugal | Marcelo |
| France | Emmanuel |
| Norway | Harald |

**`prime_ministers`**

| country | prime_minister |
|---|---|
| Portugal | Luis |
| France | François |
| Japan | Shigeru |

### Query

`SELECT p.country, p.president, pm.prime_minister FROM presidents AS p INNER JOIN prime_ministers AS pm ON p.country = pm.country;`

### Result Table

| country | president | prime_minister |
|---|---|---|
| Portugal | Marcelo | Luis |
| France | Emmanuel | François |

**Key:** Only countries found in both tables are returned.

---

## 2. LEFT JOIN Example

### Main Tables

**`left_table`**

| id | name |
|---:|---|
| 1 | A |
| 2 | B |
| 3 | C |

**`right_table`**

| id | value |
|---:|---|
| 2 | X |
| 3 | Y |
| 4 | Z |

### Query

`SELECT l.id, l.name, r.value FROM left_table AS l LEFT JOIN right_table AS r ON l.id = r.id;`

### Result Table

| id | name | value |
|---:|---|---|
| 1 | A | NULL |
| 2 | B | X |
| 3 | C | Y |

**Key:** Every record from the left table is retained.

---

## 3. RIGHT JOIN Example

### Main Tables

**`left_table`**

| id | name |
|---:|---|
| 1 | A |
| 2 | B |
| 3 | C |

**`right_table`**

| id | value |
|---:|---|
| 2 | X |
| 3 | Y |
| 4 | Z |

### Query

`SELECT l.id, l.name, r.value FROM left_table AS l RIGHT JOIN right_table AS r ON l.id = r.id;`

### Result Table

| id | name | value |
|---:|---|---|
| 2 | B | X |
| 3 | C | Y |
| 4 | NULL | Z |

**Key:** Every record from the right table is retained.

---

## 4. FULL JOIN Example

### Main Tables

**`left_table`**

| id | name |
|---:|---|
| 1 | A |
| 2 | B |
| 3 | C |

**`right_table`**

| id | value |
|---:|---|
| 2 | X |
| 3 | Y |
| 4 | Z |

### Query

`SELECT l.id, l.name, r.value FROM left_table AS l FULL JOIN right_table AS r ON l.id = r.id;`

### Result Table

| id | name | value |
|---:|---|---|
| 1 | A | NULL |
| 2 | B | X |
| 3 | C | Y |
| 4 | NULL | Z |

**Key:** All records from both tables are retained.

---

## 5. CROSS JOIN Example

### Main Tables

**`table1`**

| id |
|---:|
| 1 |
| 2 |
| 3 |

**`table2`**

| id |
|---|
| A |
| B |
| C |

### Query

`SELECT * FROM table1 CROSS JOIN table2;`

### Result Table

| table1.id | table2.id |
|---:|---|
| 1 | A |
| 1 | B |
| 1 | C |
| 2 | A |
| 2 | B |
| 2 | C |
| 3 | A |
| 3 | B |
| 3 | C |

**Key:** `3 × 3 = 9` possible combinations.

---

## 6. SELF JOIN Example

### Main Table

**`prime_ministers`**

| country | continent |
|---|---|
| Portugal | Europe |
| France | Europe |
| Germany | Europe |
| Japan | Asia |

### Query

`SELECT p1.country AS country1, p2.country AS country2 FROM prime_ministers AS p1 INNER JOIN prime_ministers AS p2 ON p1.continent = p2.continent AND p1.country <> p2.country;`

### Result Table

| country1 | country2 |
|---|---|
| Portugal | France |
| Portugal | Germany |
| France | Portugal |
| France | Germany |
| Germany | Portugal |
| Germany | France |

**Key:** Countries from the same continent are paired, but a country is not paired with itself.

---

## 7. UNION Example

### Main Tables

**`monarchs`**

| country | leader |
|---|---|
| Oman | Haitham |
| Norway | Harald |

**`prime_ministers`**

| country | leader |
|---|---|
| Oman | Haitham |
| Norway | Jonas |

### Query

`SELECT country, leader FROM monarchs UNION SELECT country, leader FROM prime_ministers;`

### Result Table

| country | leader |
|---|---|
| Oman | Haitham |
| Norway | Harald |
| Norway | Jonas |

**Key:** The identical Oman record appears only once.

---

## 8. UNION ALL Example

### Main Tables

**`monarchs`**

| country | leader |
|---|---|
| Oman | Haitham |
| Norway | Harald |

**`prime_ministers`**

| country | leader |
|---|---|
| Oman | Haitham |
| Norway | Jonas |

### Query

`SELECT country, leader FROM monarchs UNION ALL SELECT country, leader FROM prime_ministers;`

### Result Table

| country | leader |
|---|---|
| Oman | Haitham |
| Norway | Harald |
| Oman | Haitham |
| Norway | Jonas |

**Key:** Duplicate Oman record is retained.

---

## 9. INTERSECT Example

### Main Tables

**`prime_ministers`**

| country |
|---|
| Portugal |
| France |
| Norway |

**`presidents`**

| country |
|---|
| Portugal |
| France |
| Japan |

### Query

`SELECT country FROM prime_ministers INTERSECT SELECT country FROM presidents;`

### Result Table

| country |
|---|
| Portugal |
| France |

**Key:** Only records present in both result sets are returned.

---

## 10. EXCEPT Example

### Main Tables

**`monarchs`**

| country | leader |
|---|---|
| Oman | Haitham |
| Brunei | Hassanal |
| Norway | Harald |
| Spain | Felipe |

**`prime_ministers`**

| country | leader |
|---|---|
| Oman | Haitham |
| Brunei | Hassanal |
| Norway | Jonas |

### Query

`SELECT country, leader FROM monarchs EXCEPT SELECT country, leader FROM prime_ministers;`

### Result Table

| country | leader |
|---|---|
| Norway | Harald |
| Spain | Felipe |

**Key:** Only complete records in the left result that do not occur in the right result remain.

---

## 11. Semi Join / Subquery in WHERE Example

### Main Tables

**`states`**

| country | indep_year |
|---|---:|
| Spain | 1492 |
| Portugal | 1143 |
| USA | 1776 |
| Chile | 1818 |

**`presidents`**

| country | president |
|---|---|
| Portugal | Luis |
| USA | Donald |
| Chile | Gabriel |

### Query

`SELECT country, continent, president FROM presidents WHERE country IN (SELECT country FROM states WHERE indep_year < 1800);`

### Subquery Result

| country |
|---|
| Spain |
| Portugal |
| USA |

### Final Result Table

| country | president |
|---|---|
| Portugal | Luis |
| USA | Donald |

**Key:** The subquery creates the list used to filter the first table.

---

## 12. Anti Join / `NOT IN` Example

### Main Tables

**`states`**

| country | continent | indep_year |
|---|---|---:|
| USA | Americas | 1776 |
| Chile | Americas | 1818 |
| Uruguay | Americas | 1828 |
| France | Europe | 1789 |

**`presidents`**

| country | president |
|---|---|
| USA | Donald |
| Chile | Gabriel |
| Uruguay | Yamandú |

### Query

`SELECT country, president FROM presidents WHERE country NOT IN (SELECT country FROM states WHERE indep_year <= 1800) AND country IN (SELECT country FROM states WHERE continent = 'Americas');`

### Result Table

| country | president |
|---|---|
| Chile | Gabriel |
| Uruguay | Yamandú |

**Key:** Matching countries from the exclusion list are removed.

---

## 13. Subquery Inside SELECT Example

### Main Tables

**`states`**

| continent |
|---|
| Europe |
| Asia |
| Americas |

**`monarchs`**

| continent | monarch |
|---|---|
| Europe | Harald |
| Europe | Felipe |
| Asia | Naruhito |

### Query

`SELECT DISTINCT continent, (SELECT COUNT(*) FROM monarchs WHERE monarchs.continent = states.continent) AS monarch_count FROM states;`

### Result Table

| continent | monarch_count |
|---|---:|
| Europe | 2 |
| Asia | 1 |
| Americas | 0 |

**Key:** The subquery calculates the number of monarchs for each continent and requires an alias such as `monarch_count`.

---

## 14. Subquery Inside FROM Example

### Main Table

**`states`**

| continent | indep_year |
|---|---:|
| Europe | 1492 |
| Europe | 1789 |
| Europe | 1821 |
| Asia | 1946 |
| Asia | 1965 |

### Subquery Result / Temporary Table

`SELECT continent, MAX(indep_year) AS most_recent FROM states GROUP BY continent;`

| continent | most_recent |
|---|---:|
| Europe | 1821 |
| Asia | 1965 |

### Main Table

**`monarchs`**

| continent | monarch |
|---|---|
| Europe | Harald |
| Europe | Felipe |
| Asia | Naruhito |

### Final Query

`SELECT DISTINCT m.continent, sub.most_recent FROM monarchs AS m, (SELECT continent, MAX(indep_year) AS most_recent FROM states GROUP BY continent) AS sub WHERE m.continent = sub.continent ORDER BY m.continent;`

### Final Result Table

| continent | most_recent |
|---|---:|
| Asia | 1965 |
| Europe | 1821 |

**Key:** The subquery acts as a **temporary table** in the `FROM` clause and is referenced through its alias `sub`.

# 🧠 FINAL MEMORY MAP

| Concept | Remember |
|---|---|
| `INNER JOIN` | Matching rows only |
| `LEFT JOIN` | All left + matching right |
| `RIGHT JOIN` | All right + matching left |
| `FULL JOIN` | All rows from both |
| `CROSS JOIN` | Every possible combination |
| `SELF JOIN` | Table joined to itself using aliases |
| `UNION` | Both + remove duplicates |
| `UNION ALL` | Both + keep duplicates |
| `INTERSECT` | Common records |
| `EXCEPT` | Left but not right |
| Semi join | `IN (subquery)` |
| Anti join | `NOT IN (subquery)` |
| Subquery in `WHERE` | Filter |
| Subquery in `SELECT` | Calculate/return a value |
| Subquery in `FROM` | Temporary table |
| `DISTINCT` | Remove duplicate result rows |
| `<>` | Not equal |
| `ON` | Join matching condition |
| `USING` | Join shortcut for same-named fields |
