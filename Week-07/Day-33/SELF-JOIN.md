# SQL SELF JOIN

## 1. What is SQL SELF JOIN?

A **SELF JOIN** is a regular SQL JOIN in which a table is joined with **itself**.

In other words:

```text
Same table
    +
Same table
    ↓
SELF JOIN
```

A Self Join is useful when rows in the same table have a relationship with other rows in that same table.

---

# 2. Simple Definition

> **A SELF JOIN is a join where a table is joined with itself using different table aliases.**

For example:

```text
Customers
    ↙   ↘
   A     B
```

Both `A` and `B` refer to the same `Customers` table.

---

# 3. Why Do We Need Aliases?

When we use the same table twice in a query, SQL needs a way to distinguish between the two references.

Therefore, we use aliases.

For example:

```sql
FROM Customers A, Customers B
```

Here:

```text
A → first reference to Customers
B → second reference to Customers
```

Both refer to the same physical table.

---

# 4. SELF JOIN Syntax

The traditional syntax is:

```sql
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;
```

Here:

```text
T1 → alias for the first copy/reference
T2 → alias for the second copy/reference
```

The two aliases refer to the same table.

---

# 5. Modern SELF JOIN Syntax

Although the comma syntax works, it is generally clearer to use explicit `JOIN` syntax:

```sql
SELECT column_name(s)
FROM table1 AS T1
JOIN table1 AS T2
ON condition;
```

Example:

```sql
SELECT
    A.CustomerName,
    B.CustomerName
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City;
```

This is a Self Join because:

```text
Customers A
     JOIN
Customers B
```

Both are references to the same table.

---

# 6. Demo Database

Consider the following `Customers` table.

| CustomerID | CustomerName                       | ContactName    | Address                       | City        | PostalCode | Country |
| ---------: | ---------------------------------- | -------------- | ----------------------------- | ----------- | ---------- | ------- |
|          1 | Alfreds Futterkiste                | Maria Anders   | Obere Str. 57                 | Berlin      | 12209      | Germany |
|          2 | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico  |
|          3 | Antonio Moreno Taquería            | Antonio Moreno | Mataderos 2312                | México D.F. | 05023      | Mexico  |

Suppose there are additional customers in the table.

We want to find:

> **Customers who are from the same city.**

This is a perfect Self Join example.

---

# 7. SELF JOIN Example

The query can be written as:

```sql
SELECT
    A.CustomerName AS CustomerName1,
    B.CustomerName AS CustomerName2,
    A.City
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
WHERE A.CustomerID <> B.CustomerID
ORDER BY A.City;
```

This joins:

```text
Customers A
       +
Customers B
```

where:

```text
A.City = B.City
```

and:

```text
A.CustomerID <> B.CustomerID
```

ensures that a customer is not matched with itself.

---

# 8. Understanding the Query

Let's break the query into parts.

```sql
SELECT
    A.CustomerName AS CustomerName1,
    B.CustomerName AS CustomerName2,
    A.City
```

We are selecting:

```text
A.CustomerName → first customer
B.CustomerName → second customer
A.City         → common city
```

---

# 9. FROM Clause

```sql
FROM Customers AS A
```

This creates the first reference:

```text
A → Customers
```

Then:

```sql
JOIN Customers AS B
```

creates the second reference:

```text
B → Customers
```

Therefore:

```text
A → Customers
B → Customers
```

Same physical table.

---

# 10. ON Condition

```sql
ON A.City = B.City
```

This says:

> Match rows where both customers are from the same city.

For example:

```text
A.City = Mexico D.F.
B.City = Mexico D.F.
```

This is a match.

---

# 11. Why A.CustomerID <> B.CustomerID?

Without this condition, a customer could be matched with itself.

For example:

```text
Ana Trujillo
    ↔
Ana Trujillo
```

We don't want this.

Therefore:

```sql
WHERE A.CustomerID <> B.CustomerID
```

means:

> The two rows must belong to different customers.

---

# 12. Example Data

Suppose the table contains:

| CustomerID | CustomerName            | City        |
| ---------: | ----------------------- | ----------- |
|          1 | Alfreds Futterkiste     | Berlin      |
|          2 | Ana Trujillo            | Mexico D.F. |
|          3 | Antonio Moreno          | Mexico D.F. |
|          4 | Around the Horn         | London      |
|          5 | Berglunds snabbköp      | Luleå       |
|          6 | Another Mexico Customer | Mexico D.F. |

Now execute:

```sql
SELECT
    A.CustomerName AS CustomerName1,
    B.CustomerName AS CustomerName2,
    A.City
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
WHERE A.CustomerID <> B.CustomerID
ORDER BY A.City;
```

The result can contain:

| CustomerName1           | CustomerName2           | City        |
| ----------------------- | ----------------------- | ----------- |
| Ana Trujillo            | Antonio Moreno          | Mexico D.F. |
| Ana Trujillo            | Another Mexico Customer | Mexico D.F. |
| Antonio Moreno          | Ana Trujillo            | Mexico D.F. |
| Antonio Moreno          | Another Mexico Customer | Mexico D.F. |
| Another Mexico Customer | Ana Trujillo            | Mexico D.F. |
| Another Mexico Customer | Antonio Moreno          | Mexico D.F. |

---

# 13. Why Do We Get Both Directions?

Notice:

```text
Ana → Antonio
```

and:

```text
Antonio → Ana
```

Both are returned.

Why?

Because:

```text
A = Ana
B = Antonio
```

is one valid combination.

And:

```text
A = Antonio
B = Ana
```

is another valid combination.

The condition:

```sql
A.City = B.City
```

is true in both cases.

---

# 14. Avoiding Duplicate Pairs

If we only want each pair once, use:

```sql
A.CustomerID < B.CustomerID
```

instead of:

```sql
A.CustomerID <> B.CustomerID
```

Example:

```sql
SELECT
    A.CustomerName AS CustomerName1,
    B.CustomerName AS CustomerName2,
    A.City
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
WHERE A.CustomerID < B.CustomerID
ORDER BY A.City;
```

Now:

```text
Ana → Antonio
```

will be returned.

But:

```text
Antonio → Ana
```

will not be returned.

---

# 15. Why Does `<` Remove the Reverse Pair?

Suppose:

```text
Ana CustomerID = 2
Antonio CustomerID = 3
```

Condition:

```sql
A.CustomerID < B.CustomerID
```

For:

```text
A = Ana
B = Antonio
```

we get:

```text
2 < 3
```

True.

For:

```text
A = Antonio
B = Ana
```

we get:

```text
3 < 2
```

False.

Therefore only one pair remains.

---

# 16. `<>` vs `<`

This is an important Self Join concept.

### Using `<>`

```sql
WHERE A.CustomerID <> B.CustomerID
```

Returns:

```text
A → B
B → A
```

So each pair can appear twice.

---

### Using `<`

```sql
WHERE A.CustomerID < B.CustomerID
```

Returns:

```text
A → B
```

but not:

```text
B → A
```

This is useful when you want **unique pairs**.

---

# 17. Self Join Visual Explanation

Suppose:

```text
Customers

ID | Name
---+---------
1  | John
2  | David
3  | Sarah
```

A Self Join creates two logical references:

```text
Customers A

1 John
2 David
3 Sarah
```

and:

```text
Customers B

1 John
2 David
3 Sarah
```

Conceptually SQL compares rows from A with rows from B.

```text
       B
       1      2      3
A  1  John   John   John
   2  David  David  David
   3  Sarah  Sarah  Sarah
```

The join condition decides which combinations are returned.

---

# 18. SELF JOIN Does Not Create a New Table

This is important.

When we write:

```sql
FROM Customers A
JOIN Customers B
```

we are **not creating two physical tables**.

There is still only one physical table:

```text
Customers
```

We are simply giving it two aliases:

```text
A
B
```

for the purpose of the query.

---

# 19. Common SELF JOIN Use Cases

Self Join is useful when records in the same table are related to one another.

Common examples include:

* Employee → Manager relationships
* Customers from the same city
* Employees in the same department
* Products in the same category
* Finding duplicate records
* Finding people with the same attributes
* Comparing rows within the same table
* Finding hierarchical relationships
* Comparing dates or values between rows
* Finding pairs of related records

---

# 20. Most Important Example — Employee and Manager

A classic Self Join example is an employee table.

Consider:

| EmployeeID | EmployeeName | ManagerID |
| ---------: | ------------ | --------: |
|          1 | John         |      NULL |
|          2 | David        |         1 |
|          3 | Sarah        |         1 |
|          4 | Mike         |         2 |
|          5 | Lisa         |         2 |

Here:

```text
EmployeeID
     ↓
ManagerID
```

Both IDs refer to the same `Employees` table.

This means:

```text
John
 ├── David
 │    ├── Mike
 │    └── Lisa
 │
 └── Sarah
```

This is a perfect Self Join situation.

---

# 21. Employee-Manger SELF JOIN

Query:

```sql
SELECT
    E.EmployeeName AS Employee,
    M.EmployeeName AS Manager
FROM Employees AS E
LEFT JOIN Employees AS M
ON E.ManagerID = M.EmployeeID;
```

Here:

```text
E → Employee
M → Manager
```

But both are references to:

```text
Employees
```

---

# 22. Employee-Manger Result

Result:

| Employee | Manager |
| -------- | ------- |
| John     | NULL    |
| David    | John    |
| Sarah    | John    |
| Mike     | David   |
| Lisa     | David   |

This tells us:

```text
David → Manager = John
Sarah → Manager = John
Mike  → Manager = David
Lisa  → Manager = David
```

---

# 23. Why LEFT JOIN is Often Used in Employee Self Joins

The top-level manager may not have a manager.

For example:

```text
John
ManagerID = NULL
```

If we use:

```sql
INNER JOIN
```

John could disappear because there is no matching manager.

Using:

```sql
LEFT JOIN
```

keeps John:

```text
John → NULL
```

Therefore, hierarchical Self Joins commonly use `LEFT JOIN`.

---

# 24. Customer Same-City Example

The original example can be written using explicit JOIN syntax:

```sql
SELECT
    A.CustomerName AS CustomerName1,
    B.CustomerName AS CustomerName2,
    A.City
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
WHERE A.CustomerID <> B.CustomerID
ORDER BY A.City;
```

This is a Self Join because:

```text
A → Customers
B → Customers
```

---

# 25. Traditional Comma Syntax

The same query can be written using the traditional syntax:

```sql
SELECT
    A.CustomerName AS CustomerName1,
    B.CustomerName AS CustomerName2,
    A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City
ORDER BY A.City;
```

This works because the relationship is specified in the `WHERE` clause.

---

# 26. Explicit JOIN Syntax is Recommended

The traditional syntax:

```sql
FROM Customers A, Customers B
WHERE A.City = B.City
```

is valid.

But modern SQL generally favors:

```sql
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
```

Why?

Because it clearly separates:

```text
JOIN relationship
```

from:

```text
FILTER conditions
```

This makes complex queries easier to read and maintain.

---

# 27. SELF JOIN for Same Country

Suppose we want to find customers from the same country.

```sql
SELECT
    A.CustomerName AS Customer1,
    B.CustomerName AS Customer2,
    A.Country
FROM Customers AS A
JOIN Customers AS B
ON A.Country = B.Country
WHERE A.CustomerID < B.CustomerID
ORDER BY A.Country;
```

This finds unique customer pairs from the same country.

---

# 28. SELF JOIN for Same Postal Code

We can also compare postal codes.

```sql
SELECT
    A.CustomerName AS Customer1,
    B.CustomerName AS Customer2,
    A.PostalCode
FROM Customers AS A
JOIN Customers AS B
ON A.PostalCode = B.PostalCode
WHERE A.CustomerID < B.CustomerID;
```

This identifies different customers sharing the same postal code.

---

# 29. SELF JOIN for Duplicate Values

Suppose a table contains duplicate email addresses.

```text
CustomerID | Email
-----------+------------------
1          | john@example.com
2          | david@example.com
3          | john@example.com
```

A Self Join can identify matching email addresses:

```sql
SELECT
    A.CustomerID AS Customer1,
    B.CustomerID AS Customer2,
    A.Email
FROM Customers AS A
JOIN Customers AS B
ON A.Email = B.Email
WHERE A.CustomerID < B.CustomerID;
```

Result:

| Customer1 | Customer2 | Email                                       |
| --------: | --------: | ------------------------------------------- |
|         1 |         3 | [john@example.com](mailto:john@example.com) |

This shows that customer IDs `1` and `3` have the same email.

---

# 30. SELF JOIN for Comparing Values

Suppose we have:

| EmployeeID | EmployeeName | Salary |
| ---------: | ------------ | -----: |
|          1 | John         |  50000 |
|          2 | David        |  60000 |
|          3 | Sarah        |  70000 |

We can find employee pairs where one employee earns more than another:

```sql
SELECT
    A.EmployeeName AS Employee1,
    B.EmployeeName AS Employee2,
    A.Salary AS Salary1,
    B.Salary AS Salary2
FROM Employees AS A
JOIN Employees AS B
ON A.Salary > B.Salary;
```

This compares rows within the same table.

---

# 31. SELF JOIN for Employees in Same Department

Suppose:

| EmployeeID | EmployeeName | DepartmentID |
| ---------: | ------------ | -----------: |
|          1 | John         |           10 |
|          2 | David        |           10 |
|          3 | Sarah        |           20 |
|          4 | Mike         |           10 |

Query:

```sql
SELECT
    A.EmployeeName AS Employee1,
    B.EmployeeName AS Employee2,
    A.DepartmentID
FROM Employees AS A
JOIN Employees AS B
ON A.DepartmentID = B.DepartmentID
WHERE A.EmployeeID < B.EmployeeID;
```

Result conceptually:

| Employee1 | Employee2 | DepartmentID |
| --------- | --------- | -----------: |
| John      | David     |           10 |
| John      | Mike      |           10 |
| David     | Mike      |           10 |

Each employee pair is returned only once.

---

# 32. SELF JOIN and Hierarchical Data

Self Joins are particularly important for hierarchical data.

Example:

```text
Company
   │
   ├── CEO
   │
   ├── Manager
   │      ├── Employee
   │      └── Employee
   │
   └── Manager
          ├── Employee
          └── Employee
```

A table can store the hierarchy using:

```text
EmployeeID
ManagerID
```

For example:

| EmployeeID | EmployeeName | ManagerID |
| ---------: | ------------ | --------: |
|          1 | CEO          |      NULL |
|          2 | Manager A    |         1 |
|          3 | Manager B    |         1 |
|          4 | Employee A   |         2 |
|          5 | Employee B   |         2 |

The `ManagerID` points back to:

```text
Employees.EmployeeID
```

That is a **self-referencing relationship**.

---

# 33. Self-Referencing Foreign Key

The employee table may have:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    ManagerID INT,
    FOREIGN KEY (ManagerID)
        REFERENCES Employees(EmployeeID)
);
```

Notice:

```sql
REFERENCES Employees(EmployeeID)
```

The table references itself.

This creates a self-referencing relationship.

---

# 34. Querying a Self-Referencing Table

```sql
SELECT
    E.EmployeeName AS Employee,
    M.EmployeeName AS Manager
FROM Employees AS E
LEFT JOIN Employees AS M
ON E.ManagerID = M.EmployeeID;
```

Logical interpretation:

```text
E.ManagerID
     ↓
M.EmployeeID
```

Therefore:

```text
Employee's ManagerID
        matches
Manager's EmployeeID
```

---

# 35. SELF JOIN vs Normal JOIN

Normal JOIN:

```text
Table A
   JOIN
Table B
```

Self Join:

```text
Table A
   JOIN
Table A
```

The difference is:

| Type        | Tables                      |
| ----------- | --------------------------- |
| Normal JOIN | Two different tables        |
| SELF JOIN   | Same table referenced twice |

---

# 36. SELF JOIN vs CROSS JOIN

These are different.

### SELF JOIN

A Self Join has a relationship condition.

```sql
SELECT *
FROM Customers A
JOIN Customers B
ON A.City = B.City;
```

### CROSS JOIN

A Cross Join intentionally creates the Cartesian product.

```sql
SELECT *
FROM Customers A
CROSS JOIN Customers B;
```

For `N` rows, a Cross Join can produce:

```text
N × N
```

combinations.

A Self Join may also generate many combinations depending on its condition, but the purpose and semantics are different.

---

# 37. SELF JOIN and Number of Combinations

Suppose a city has:

```text
3 customers
```

Using:

```sql
WHERE A.CustomerID <> B.CustomerID
```

the possible ordered pairs are:

```text
3 × 2 = 6
```

For example:

```text
A → B
A → C
B → A
B → C
C → A
C → B
```

Using:

```sql
WHERE A.CustomerID < B.CustomerID
```

we get:

```text
3
```

unique pairs:

```text
A → B
A → C
B → C
```

The number of unique pairs among `N` rows is:

```text
N × (N - 1) / 2
```

---

# 38. Important SELF JOIN Pattern

When finding unique pairs, remember:

```sql
WHERE A.ID < B.ID
```

This is a very useful pattern.

For example:

```sql
SELECT
    A.Name,
    B.Name
FROM Employees AS A
JOIN Employees AS B
ON A.DepartmentID = B.DepartmentID
WHERE A.EmployeeID < B.EmployeeID;
```

This prevents:

```text
A → B
B → A
```

from both appearing.

---

# 39. SELF JOIN with ORDER BY

Example:

```sql
SELECT
    A.CustomerName AS Customer1,
    B.CustomerName AS Customer2,
    A.City
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
WHERE A.CustomerID < B.CustomerID
ORDER BY A.City, A.CustomerName;
```

The result is first sorted by city and then customer name.

---

# 40. SELF JOIN with Multiple Conditions

A Self Join can have multiple conditions.

```sql
SELECT
    A.CustomerName AS Customer1,
    B.CustomerName AS Customer2
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
AND A.Country = B.Country
WHERE A.CustomerID < B.CustomerID;
```

This means:

```text
Same City
    AND
Same Country
```

and:

```text
Different CustomerID
```

---

# 41. SELF JOIN with LEFT JOIN

Self Join does not necessarily mean `INNER JOIN`.

You can use:

```sql
LEFT JOIN
```

Example:

```sql
SELECT
    E.EmployeeName AS Employee,
    M.EmployeeName AS Manager
FROM Employees AS E
LEFT JOIN Employees AS M
ON E.ManagerID = M.EmployeeID;
```

This is still a Self Join.

The key idea is:

```text
Same table is referenced more than once.
```

---

# 42. SELF JOIN with RIGHT JOIN

You can technically use:

```sql
RIGHT JOIN
```

as well:

```sql
SELECT
    E.EmployeeName AS Employee,
    M.EmployeeName AS Manager
FROM Employees AS E
RIGHT JOIN Employees AS M
ON E.ManagerID = M.EmployeeID;
```

Again:

```text
E → Employees
M → Employees
```

Therefore it is a Self Join.

---

# 43. SELF JOIN with FULL JOIN

A Self Join can also use FULL JOIN in database systems that support it.

```sql
SELECT
    A.EmployeeName,
    B.EmployeeName
FROM Employees AS A
FULL JOIN Employees AS B
ON A.DepartmentID = B.DepartmentID;
```

However, this is less common than `INNER JOIN` or `LEFT JOIN` Self Join patterns.

---

# 44. SELF JOIN with DELETE

Self Join can sometimes be useful when deleting duplicate records.

For example, conceptually:

```sql
DELETE FROM Customers
WHERE CustomerID IN (
    SELECT A.CustomerID
    FROM Customers AS A
    JOIN Customers AS B
    ON A.Email = B.Email
    WHERE A.CustomerID > B.CustomerID
);
```

This type of operation must be handled carefully because SQL behavior around modifying and reading the same table can vary by database system.

Always test the corresponding `SELECT` first.

---

# 45. SELF JOIN with UPDATE

Self Join can also be useful for updating rows based on another row in the same table.

The exact syntax varies by database system.

The general idea is:

```text
Row A
  ↓
compare with
  ↓
Row B
  ↓
update Row A
```

This is another example of why Self Join is useful for row-to-row comparisons.

---

# 46. SELF JOIN vs Window Functions

Some problems that can be solved with Self Join can also be solved using window functions.

For example:

```text
Compare current row with another row
```

can sometimes be handled using:

```sql
LAG()
LEAD()
ROW_NUMBER()
RANK()
```

Self Join is still important because it directly demonstrates relationships between rows.

---

# 47. Common Mistakes

## Mistake 1 — Not using aliases

Incorrect or ambiguous:

```sql
SELECT CustomerName
FROM Customers
JOIN Customers
ON CustomerID = CustomerID;
```

SQL cannot reliably determine which reference you mean.

Better:

```sql
SELECT
    A.CustomerName,
    B.CustomerName
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City;
```

---

# 48. Common Mistake — Forgetting the Self-Match

Suppose:

```sql
SELECT
    A.CustomerName,
    B.CustomerName
FROM Customers A
JOIN Customers B
ON A.City = B.City;
```

A customer can match itself.

For example:

```text
Ana → Ana
Antonio → Antonio
```

If you don't want this, add:

```sql
WHERE A.CustomerID <> B.CustomerID
```

---

# 49. Common Mistake — Getting Duplicate Pairs

Using:

```sql
WHERE A.CustomerID <> B.CustomerID
```

can produce:

```text
Ana → Antonio
Antonio → Ana
```

If only one pair is required, use:

```sql
WHERE A.CustomerID < B.CustomerID
```

---

# 50. Common Mistake — Confusing Alias with Another Table

In:

```sql
FROM Customers A
JOIN Customers B
```

`A` and `B` are **not different physical tables**.

They are aliases:

```text
A → Customers
B → Customers
```

There is still only one physical table.

---

# 51. Practical Example — Find Employees Who Earn More Than Others

Employees:

| EmployeeID | EmployeeName | Salary |
| ---------: | ------------ | -----: |
|          1 | John         |  50000 |
|          2 | David        |  60000 |
|          3 | Sarah        |  70000 |

Query:

```sql
SELECT
    A.EmployeeName AS HigherPaidEmployee,
    B.EmployeeName AS LowerPaidEmployee,
    A.Salary AS HigherSalary,
    B.Salary AS LowerSalary
FROM Employees AS A
JOIN Employees AS B
ON A.Salary > B.Salary;
```

Conceptually:

```text
David > John
Sarah > John
Sarah > David
```

This compares rows within the same table.

---

# 52. Practical Example — Find Customers from Same City

```sql
SELECT
    A.CustomerName AS Customer1,
    B.CustomerName AS Customer2,
    A.City
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
WHERE A.CustomerID < B.CustomerID
ORDER BY A.City;
```

Meaning:

```text
Take Customer A
        ↓
Take Customer B
        ↓
Compare their City
        ↓
If same city
        ↓
Return the pair
```

---

# 53. Practical Example — Employee and Manager

```sql
SELECT
    E.EmployeeName AS Employee,
    M.EmployeeName AS Manager
FROM Employees AS E
LEFT JOIN Employees AS M
ON E.ManagerID = M.EmployeeID;
```

Meaning:

```text
Employee.ManagerID
        ↓
matches
        ↓
Manager.EmployeeID
```

Result:

```text
Employee → Manager
```

This is one of the most important real-world Self Join examples.

---

# 54. Practical Example — Find People with Same Country

```sql
SELECT
    A.CustomerName AS Customer1,
    B.CustomerName AS Customer2,
    A.Country
FROM Customers AS A
JOIN Customers AS B
ON A.Country = B.Country
WHERE A.CustomerID < B.CustomerID
ORDER BY A.Country;
```

The `<` condition ensures each pair is returned once.

---

# 55. Practical Example — Find Duplicate Emails

```sql
SELECT
    A.CustomerID AS Customer1,
    B.CustomerID AS Customer2,
    A.Email
FROM Customers AS A
JOIN Customers AS B
ON A.Email = B.Email
WHERE A.CustomerID < B.CustomerID;
```

This finds different customer records with the same email.

---

# 56. SELF JOIN Mental Model

Think of Self Join as:

```text
             ONE TABLE

          ┌───────────────┐
          │   Customers   │
          └───────────────┘
             ↙         ↘
            A           B
             \         /
              \       /
               JOIN
```

The database treats:

```text
A
```

and:

```text
B
```

as two logical references to the same table.

---

# 57. SELF JOIN Formula

The basic idea is:

```text
SELF JOIN
=
Same Table
+
Two Aliases
+
Relationship Between Rows
```

For example:

```sql
FROM Customers A
JOIN Customers B
ON A.City = B.City
```

means:

```text
Customers A
    ↓
compare
    ↓
Customers B
```

---

# 58. SELF JOIN Cheat Sheet

### Basic Self Join

```sql
SELECT *
FROM TableA AS A
JOIN TableA AS B
ON A.column = B.column;
```

### Exclude Same Row

```sql
SELECT *
FROM TableA AS A
JOIN TableA AS B
ON A.column = B.column
WHERE A.id <> B.id;
```

### Unique Pairs

```sql
SELECT *
FROM TableA AS A
JOIN TableA AS B
ON A.column = B.column
WHERE A.id < B.id;
```

### Employee → Manager

```sql
SELECT
    E.EmployeeName AS Employee,
    M.EmployeeName AS Manager
FROM Employees AS E
LEFT JOIN Employees AS M
ON E.ManagerID = M.EmployeeID;
```

### Same City

```sql
SELECT
    A.CustomerName AS Customer1,
    B.CustomerName AS Customer2,
    A.City
FROM Customers AS A
JOIN Customers AS B
ON A.City = B.City
WHERE A.CustomerID < B.CustomerID;
```

---

# 59. SELF JOIN — Key Points

1. A Self Join joins a table with **itself**.

2. It is not a special SQL JOIN keyword.

3. It uses normal JOIN operations.

4. Aliases are used to distinguish the two references.

5. Example:

```sql
Customers AS A
JOIN Customers AS B
```

6. `A` and `B` represent the same physical table.

7. Self Joins are useful for comparing rows within the same table.

8. Self Joins are commonly used for hierarchical data.

9. Employee-manager relationships are a classic example.

10. Self Joins can find customers from the same city.

11. Self Joins can find employees in the same department.

12. Self Joins can identify duplicate values.

13. `A.ID <> B.ID` prevents a row from matching itself.

14. `A.ID < B.ID` prevents reverse duplicate pairs.

15. Self Joins can use `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and, where supported, `FULL JOIN`.

---

# 60. Final Memory Trick

Remember:

```text
NORMAL JOIN

Table A
   JOIN
Table B


SELF JOIN

Table A
   JOIN
Table A
```

But SQL gives the two references different aliases:

```text
Table A AS X
      JOIN
Table A AS Y
```

Therefore:

```text
X → first reference
Y → second reference
```

And the most important idea:

```text
SELF JOIN
    =
SAME TABLE
    +
TWO ALIASES
    +
ROW-TO-ROW COMPARISON
```

### One-Line Definition

> **A SQL Self Join is a regular JOIN where the same table is referenced more than once using different aliases, allowing rows within that table to be compared or related to each other.**
