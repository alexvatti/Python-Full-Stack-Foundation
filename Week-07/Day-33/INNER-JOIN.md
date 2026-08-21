# SQL INNER JOIN

## 1. What is a SQL JOIN?

A **JOIN** is used to combine rows from **two or more tables** based on a related column between those tables.

In a relational database, data is normally divided into multiple tables to avoid duplication and maintain relationships.

For example, our database contains:

| Table          | Records | Purpose                      |
| -------------- | ------: | ---------------------------- |
| `Customers`    |      91 | Customer information         |
| `Categories`   |       8 | Product categories           |
| `Employees`    |      10 | Employee information         |
| `OrderDetails` |     518 | Products included in orders  |
| `Orders`       |     196 | Order information            |
| `Products`     |      77 | Product information          |
| `Shippers`     |       3 | Shipping company information |
| `Suppliers`    |      29 | Supplier information         |

Because information is distributed across these tables, we need **JOINs** to retrieve related information together.

---

# 2. Why Do We Need JOINs?

Consider these two tables.

## Customers

| CustomerID | CustomerName                       | Country |
| ---------: | ---------------------------------- | ------- |
|          1 | Alfreds Futterkiste                | Germany |
|          2 | Ana Trujillo Emparedados y helados | Mexico  |
|          3 | Antonio Moreno Taquería            | Mexico  |

## Orders

| OrderID | CustomerID | OrderDate  |
| ------: | ---------: | ---------- |
|   10248 |         90 | 1996-07-04 |
|   10249 |         81 | 1996-07-05 |
|   10308 |          2 | 1996-09-18 |
|   10365 |          3 | 1996-11-27 |

Notice that both tables contain:

```text
CustomerID
```

This column establishes the relationship between the tables.

For example:

```text
Customers
    |
    | CustomerID
    |
    +----------------+
                     |
                     |
                  Orders
```

Customer `2` in the `Customers` table can be connected to orders having `CustomerID = 2` in the `Orders` table.

---

# 3. Types of SQL JOINs

The major SQL JOIN types are:

| JOIN              | Meaning                                                               |
| ----------------- | --------------------------------------------------------------------- |
| `INNER JOIN`      | Returns only matching rows from both tables                           |
| `LEFT JOIN`       | Returns all rows from the left table and matching rows from the right |
| `RIGHT JOIN`      | Returns all rows from the right table and matching rows from the left |
| `FULL OUTER JOIN` | Returns all rows when there is a match in either table                |

This document focuses on:

# `INNER JOIN`

---

# 4. What is INNER JOIN?

An `INNER JOIN` returns **only the rows that have matching values in both tables**.

In simple words:

> **INNER JOIN = Give me only the records that exist in both related tables.**

Think of it as:

```text
Table A          Table B

   A                 B
   |                 |
   |    MATCH        |
   +------ X --------+
          |
       RESULT
```

Only the matching portion is returned.

---

# 5. Basic INNER JOIN Syntax

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

The important parts are:

```sql
SELECT
```

Specifies which columns you want.

```sql
FROM table1
```

Specifies the first table.

```sql
INNER JOIN table2
```

Specifies the second table.

```sql
ON table1.column_name = table2.column_name
```

Specifies how the two tables are related.

---

# 6. First Example — Products and Categories

Our database contains:

```text
Products
Categories
```

The relationship is:

```text
Products.CategoryID
        |
        |
        v
Categories.CategoryID
```

## Products

Example:

| ProductID | ProductName   | CategoryID | Price |
| --------: | ------------- | ---------: | ----: |
|         1 | Chai          |          1 | 18.00 |
|         2 | Chang         |          1 | 19.00 |
|         3 | Aniseed Syrup |          2 | 10.00 |

## Categories

Example:

| CategoryID | CategoryName | Description                |
| ---------: | ------------ | -------------------------- |
|          1 | Beverages    | Soft drinks, coffees, teas |
|          2 | Condiments   | Sweet and savory sauces    |
|          3 | Confections  | Desserts and candies       |

The common column is:

```text
CategoryID
```

---

# 7. INNER JOIN Products and Categories

```sql
SELECT ProductID, ProductName, CategoryName
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

This query connects:

```text
Products.CategoryID
          =
Categories.CategoryID
```

The database looks for matching `CategoryID` values.

---

# 8. Understanding the Result

Suppose we have:

### Products

| ProductID | ProductName   | CategoryID |
| --------: | ------------- | ---------: |
|         1 | Chai          |          1 |
|         2 | Chang         |          1 |
|         3 | Aniseed Syrup |          2 |

### Categories

| CategoryID | CategoryName |
| ---------: | ------------ |
|          1 | Beverages    |
|          2 | Condiments   |

The JOIN produces:

| ProductID | ProductName   | CategoryName |
| --------: | ------------- | ------------ |
|         1 | Chai          | Beverages    |
|         2 | Chang         | Beverages    |
|         3 | Aniseed Syrup | Condiments   |

The JOIN has combined information from two different tables.

---

# 9. How INNER JOIN Works

Consider:

```text
Products
```

| ProductID | ProductName   | CategoryID |
| --------: | ------------- | ---------: |
|         1 | Chai          |          1 |
|         2 | Chang         |          1 |
|         3 | Aniseed Syrup |          2 |
|         4 | Product X     |         99 |

And:

```text
Categories
```

| CategoryID | CategoryName |
| ---------: | ------------ |
|          1 | Beverages    |
|          2 | Condiments   |
|          3 | Confections  |

Now execute:

```sql
SELECT ProductID, ProductName, CategoryName
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

The database checks each product:

```text
Product 1 → CategoryID 1 → MATCH
Product 2 → CategoryID 1 → MATCH
Product 3 → CategoryID 2 → MATCH
Product 4 → CategoryID 99 → NO MATCH
```

Therefore:

| ProductID | ProductName   | CategoryName |
| --------: | ------------- | ------------ |
|         1 | Chai          | Beverages    |
|         2 | Chang         | Beverages    |
|         3 | Aniseed Syrup | Condiments   |

`Product X` is not returned because:

```text
CategoryID = 99
```

does not exist in `Categories`.

---

# 10. The Most Important INNER JOIN Rule

Remember:

> **INNER JOIN returns only matching records.**

If there is no matching value:

```text
LEFT TABLE                    RIGHT TABLE

CustomerID                    CustomerID
    1                             1
    2                             2
    3                             5
```

Matching values:

```text
1 ↔ 1
2 ↔ 2
```

Result:

```text
1
2
```

Customer `3` is not returned because there is no matching `3` in the right table.

---

# 11. JOIN vs INNER JOIN

These two statements produce the same result:

```sql
SELECT Products.ProductID,
       Products.ProductName,
       Categories.CategoryName
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

and:

```sql
SELECT Products.ProductID,
       Products.ProductName,
       Categories.CategoryName
FROM Products
JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

Why?

Because:

```text
JOIN = INNER JOIN
```

`INNER` is the default JOIN type.

Therefore:

```sql
JOIN
```

is simply a shorter way of writing:

```sql
INNER JOIN
```

---

# 12. Best Practice — Use Table Names

Consider:

```sql
SELECT ProductID, ProductName, CategoryName
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

This may work because `ProductID`, `ProductName`, and `CategoryName` are unique to their respective tables.

However, it is better practice to explicitly specify the table:

```sql
SELECT Products.ProductID,
       Products.ProductName,
       Categories.CategoryName
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

This makes the query:

* Easier to read
* Easier to understand
* Less ambiguous
* Easier to maintain

---

# 13. Why Table Names Become Important

Both tables contain:

```text
CategoryID
```

Therefore, this can become ambiguous:

```sql
SELECT CategoryID
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

SQL may report an ambiguous-column error because it does not know which `CategoryID` you mean.

Instead write:

```sql
SELECT Products.CategoryID,
       Products.ProductName,
       Categories.CategoryName
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

Now SQL knows exactly which column is required.

---

# 14. Using Table Aliases

Instead of repeatedly writing full table names, we can use aliases.

Example:

```sql
SELECT P.ProductID,
       P.ProductName,
       C.CategoryName
FROM Products AS P
INNER JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

Here:

```text
P = Products
C = Categories
```

So:

```sql
P.ProductID
```

means:

```sql
Products.ProductID
```

and:

```sql
C.CategoryName
```

means:

```sql
Categories.CategoryName
```

This is very common in real-world SQL.

---

# 15. AS Is Optional for Table Aliases

Both are valid:

```sql
FROM Products AS P
INNER JOIN Categories AS C
```

and:

```sql
FROM Products P
INNER JOIN Categories C
```

Most developers use aliases because they make complex queries shorter and easier to read.

---

# 16. Example — Orders and Customers

Our database contains:

```text
Customers
Orders
```

The relationship is:

```text
Customers.CustomerID
        |
        |
        v
Orders.CustomerID
```

For example:

### Customers

| CustomerID | CustomerName                       | Country |
| ---------: | ---------------------------------- | ------- |
|          1 | Alfreds Futterkiste                | Germany |
|          2 | Ana Trujillo Emparedados y helados | Mexico  |
|          3 | Antonio Moreno Taquería            | Mexico  |

### Orders

| OrderID | CustomerID | OrderDate  |
| ------: | ---------: | ---------- |
|   10308 |          2 | 1996-09-18 |
|   10365 |          3 | 1996-11-27 |

Query:

```sql
SELECT Orders.OrderID,
       Customers.CustomerName,
       Orders.OrderDate
FROM Orders
INNER JOIN Customers
ON Orders.CustomerID = Customers.CustomerID;
```

Result:

| OrderID | CustomerName                       | OrderDate  |
| ------: | ---------------------------------- | ---------- |
|   10308 | Ana Trujillo Emparedados y helados | 1996-09-18 |
|   10365 | Antonio Moreno Taquería            | 1996-11-27 |

The JOIN allows us to display:

```text
Order information
        +
Customer information
```

even though they are stored in separate tables.

---

# 17. Why Not Store CustomerName Directly in Orders?

A beginner may ask:

> Why not simply store `CustomerName` inside the `Orders` table?

Because that would duplicate data.

For example:

```text
Orders

OrderID | CustomerID | CustomerName
------------------------------------
10308   | 2          | Ana
10309   | 2          | Ana
10310   | 2          | Ana
10311   | 2          | Ana
```

The customer name is repeated many times.

Instead, database normalization stores:

### Customers

```text
CustomerID → CustomerName
```

and:

### Orders

```text
OrderID → CustomerID
```

Then JOIN connects them when needed.

This is one of the major reasons relational databases use JOINs.

---

# 18. INNER JOIN with Three Tables

We can join more than two tables.

Our database contains:

```text
Orders
Customers
Shippers
```

Relationships:

```text
Customers
    |
    | CustomerID
    |
Orders
    |
    | ShipperID
    |
Shippers
```

The query:

```sql
SELECT Orders.OrderID,
       Customers.CustomerName,
       Shippers.ShipperName
FROM Orders
INNER JOIN Customers
ON Orders.CustomerID = Customers.CustomerID
INNER JOIN Shippers
ON Orders.ShipperID = Shippers.ShipperID;
```

This combines information from:

```text
Orders
+
Customers
+
Shippers
```

---

# 19. Understanding the Three-Table JOIN

Suppose:

### Orders

| OrderID | CustomerID | ShipperID |
| ------: | ---------: | --------: |
|   10248 |         90 |         3 |
|   10249 |         81 |         1 |
|   10308 |          2 |         2 |

### Customers

| CustomerID | CustomerName           |
| ---------: | ---------------------- |
|         90 | Wilman Kala            |
|         81 | Tradição Hipermercados |
|          2 | Ana Trujillo           |

### Shippers

| ShipperID | ShipperName      |
| --------: | ---------------- |
|         1 | Speedy Express   |
|         2 | United Package   |
|         3 | Federal Shipping |

The JOIN produces:

| OrderID | CustomerName           | ShipperName      |
| ------: | ---------------------- | ---------------- |
|   10248 | Wilman Kala            | Federal Shipping |
|   10249 | Tradição Hipermercados | Speedy Express   |
|   10308 | Ana Trujillo           | United Package   |

One SQL query has combined three tables.

---

# 20. JOIN Multiple Tables — General Pattern

The general pattern is:

```sql
SELECT ...
FROM TableA
INNER JOIN TableB
ON TableA.key = TableB.key
INNER JOIN TableC
ON TableB.key = TableC.key
INNER JOIN TableD
ON TableC.key = TableD.key;
```

You can continue adding JOINs as required.

---

# 21. INNER JOIN in Our Northwind Database

Our database has:

| Table        | Records |
| ------------ | ------: |
| Customers    |      91 |
| Categories   |       8 |
| Employees    |      10 |
| OrderDetails |     518 |
| Orders       |     196 |
| Products     |      77 |
| Shippers     |       3 |
| Suppliers    |      29 |

The important relationships include:

```text
Customers
   |
   | CustomerID
   |
Orders
   |
   | OrderID
   |
OrderDetails
   |
   | ProductID
   |
Products
   |
   | CategoryID
   |
Categories
```

There are also:

```text
Orders
   |
   | EmployeeID
   |
Employees
```

```text
Orders
   |
   | ShipperID
   |
Shippers
```

```text
Products
   |
   | SupplierID
   |
Suppliers
```

---

# 22. Important Relationships

| Parent Table | Parent Key   | Child Table    | Foreign Key  |
| ------------ | ------------ | -------------- | ------------ |
| `Customers`  | `CustomerID` | `Orders`       | `CustomerID` |
| `Employees`  | `EmployeeID` | `Orders`       | `EmployeeID` |
| `Shippers`   | `ShipperID`  | `Orders`       | `ShipperID`  |
| `Orders`     | `OrderID`    | `OrderDetails` | `OrderID`    |
| `Products`   | `ProductID`  | `OrderDetails` | `ProductID`  |
| `Categories` | `CategoryID` | `Products`     | `CategoryID` |
| `Suppliers`  | `SupplierID` | `Products`     | `SupplierID` |

These relationships are what make JOINs possible.

---

# 23. Example — Orders + Customers

```sql
SELECT O.OrderID,
       O.OrderDate,
       C.CustomerName
FROM Orders AS O
INNER JOIN Customers AS C
ON O.CustomerID = C.CustomerID;
```

Conceptually:

```text
Orders
   |
   | CustomerID
   |
   +------ JOIN ------+
                      |
                      |
                  Customers
```

Result:

```text
OrderID | OrderDate  | CustomerName
--------|------------|-------------------------
10308   | 1996-09-18 | Ana Trujillo
10365   | 1996-11-27 | Antonio Moreno
...
```

---

# 24. Example — Products + Categories

```sql
SELECT P.ProductID,
       P.ProductName,
       C.CategoryName
FROM Products AS P
INNER JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

Result:

```text
ProductID | ProductName     | CategoryName
----------|-----------------|-------------
1         | Chai            | Beverages
2         | Chang           | Beverages
3         | Aniseed Syrup   | Condiments
...
```

---

# 25. Example — Products + Suppliers

The relationship:

```text
Products.SupplierID
        =
Suppliers.SupplierID
```

Query:

```sql
SELECT P.ProductID,
       P.ProductName,
       S.SupplierName
FROM Products AS P
INNER JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID;
```

This gives:

```text
Product
   +
Supplier
```

in one result.

---

# 26. Example — Orders + Employees

The relationship:

```text
Orders.EmployeeID
        =
Employees.EmployeeID
```

Query:

```sql
SELECT O.OrderID,
       O.OrderDate,
       E.FirstName,
       E.LastName
FROM Orders AS O
INNER JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

This allows us to see which employee handled each order.

---

# 27. Example — Orders + Shippers

The relationship:

```text
Orders.ShipperID
        =
Shippers.ShipperID
```

Query:

```sql
SELECT O.OrderID,
       O.OrderDate,
       S.ShipperName
FROM Orders AS O
INNER JOIN Shippers AS S
ON O.ShipperID = S.ShipperID;
```

Result conceptually:

| OrderID | OrderDate  | ShipperName      |
| ------: | ---------- | ---------------- |
|   10248 | 1996-07-04 | Federal Shipping |
|   10249 | 1996-07-05 | Speedy Express   |
|   10308 | 1996-09-18 | United Package   |

---

# 28. Example — OrderDetails + Products

This is another important relationship:

```text
OrderDetails.ProductID
        =
Products.ProductID
```

Query:

```sql
SELECT OD.OrderID,
       OD.ProductID,
       P.ProductName,
       OD.Quantity
FROM OrderDetails AS OD
INNER JOIN Products AS P
ON OD.ProductID = P.ProductID;
```

This gives us:

```text
Order
+
Product
+
Quantity
```

---

# 29. Four-Table INNER JOIN

We can combine:

```text
Orders
Customers
OrderDetails
Products
```

Relationships:

```text
Customers
    |
    | CustomerID
    |
Orders
    |
    | OrderID
    |
OrderDetails
    |
    | ProductID
    |
Products
```

SQL:

```sql
SELECT O.OrderID,
       C.CustomerName,
       P.ProductName,
       OD.Quantity
FROM Orders AS O
INNER JOIN Customers AS C
ON O.CustomerID = C.CustomerID
INNER JOIN OrderDetails AS OD
ON O.OrderID = OD.OrderID
INNER JOIN Products AS P
ON OD.ProductID = P.ProductID;
```

This is a very important real-world JOIN pattern.

---

# 30. What Does This Query Produce?

The result could look like:

| OrderID | CustomerName           | ProductName                   | Quantity |
| ------: | ---------------------- | ----------------------------- | -------: |
|   10248 | Wilman Kala            | Queso Cabrales                |       12 |
|   10248 | Wilman Kala            | Singaporean Hokkien Fried Mee |       10 |
|   10248 | Wilman Kala            | Mozzarella di Giovanni        |        5 |
|   10249 | Tradição Hipermercados | Tofu                          |        9 |
|   10249 | Tradição Hipermercados | Manjimup Dried Apples         |       40 |

Notice something important:

An order can appear **multiple times**.

Why?

Because one order can contain multiple products.

For example:

```text
Order 10248
    |
    +--- Product A
    +--- Product B
    +--- Product C
```

Therefore:

```text
OrderID 10248
```

can appear three times in the result.

This is normal.

---

# 31. INNER JOIN Does Not Mean One Row Per Table

A common beginner misunderstanding is:

> "If I join two tables, I should get one row for every row in the first table."

Not necessarily.

The number of result rows depends on the relationship.

For example:

```text
One Customer
      |
      +--- Order 1
      +--- Order 2
      +--- Order 3
```

When Customers and Orders are joined:

```text
Customer 1 + Order 1
Customer 1 + Order 2
Customer 1 + Order 3
```

The customer appears three times.

This is because the relationship is:

```text
1 Customer → Many Orders
```

---

# 32. One-to-Many Relationship

Our database contains many one-to-many relationships.

Example:

```text
Customers
   1
   |
   | 
   |----< Orders
             Many
```

Meaning:

```text
1 Customer
      ↓
Many Orders
```

Similarly:

```text
Categories
    1
    |
    +----< Products
             Many
```

And:

```text
Orders
   1
   |
   +----< OrderDetails
             Many
```

Understanding cardinality is extremely important when learning JOINs.

---

# 33. INNER JOIN and Missing Data

Suppose:

### Products

| ProductID | ProductName | CategoryID |
| --------: | ----------- | ---------: |
|         1 | Chai        |          1 |
|         2 | Chang       |          1 |
|         3 | Product X   |       NULL |

### Categories

| CategoryID | CategoryName |
| ---------: | ------------ |
|          1 | Beverages    |
|          2 | Condiments   |

Query:

```sql
SELECT P.ProductName,
       C.CategoryName
FROM Products AS P
INNER JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

Result:

| ProductName | CategoryName |
| ----------- | ------------ |
| Chai        | Beverages    |
| Chang       | Beverages    |

`Product X` is excluded because:

```text
Product X.CategoryID = NULL
```

does not match a category.

---

# 34. INNER JOIN and Invalid Foreign Key

Suppose:

```text
Product X
CategoryID = 99
```

but:

```text
Categories
```

contains only:

```text
1
2
3
```

Then:

```sql
ON P.CategoryID = C.CategoryID
```

cannot find a match.

Therefore:

```text
Product X
```

does not appear in an INNER JOIN result.

---

# 35. INNER JOIN vs WHERE

Consider:

```sql
SELECT P.ProductName,
       C.CategoryName
FROM Products AS P
INNER JOIN Categories AS C
ON P.CategoryID = C.CategoryID
WHERE C.CategoryName = 'Beverages';
```

The process is conceptually:

```text
1. JOIN Products and Categories
              ↓
2. Find matching CategoryID
              ↓
3. Apply WHERE condition
              ↓
4. Return Beverages products
```

The JOIN determines **how tables are connected**.

The WHERE clause determines **which joined rows we want**.

---

# 36. ON vs WHERE

This distinction is very important.

### ON

Defines the relationship:

```sql
ON P.CategoryID = C.CategoryID
```

Meaning:

> Connect products to their categories.

### WHERE

Filters the result:

```sql
WHERE C.CategoryName = 'Beverages'
```

Meaning:

> After joining, keep only beverages.

Remember:

```text
ON     → How do tables connect?
WHERE  → Which rows do I want?
```

---

# 37. INNER JOIN with Filtering

Example:

```sql
SELECT P.ProductID,
       P.ProductName,
       P.Price,
       C.CategoryName
FROM Products AS P
INNER JOIN Categories AS C
ON P.CategoryID = C.CategoryID
WHERE P.Price > 20;
```

This means:

```text
Products
     +
Categories
     ↓
Match CategoryID
     ↓
Keep Price > 20
```

---

# 38. INNER JOIN with ORDER BY

We can also sort the result.

```sql
SELECT P.ProductID,
       P.ProductName,
       P.Price,
       C.CategoryName
FROM Products AS P
INNER JOIN Categories AS C
ON P.CategoryID = C.CategoryID
ORDER BY P.Price DESC;
```

This returns products with their categories and sorts them from highest price to lowest price.

---

# 39. INNER JOIN with Multiple Conditions

The `ON` clause can contain multiple conditions.

Example:

```sql
SELECT ...
FROM TableA AS A
INNER JOIN TableB AS B
ON A.ID = B.ID
AND A.Status = B.Status;
```

The JOIN requires both conditions to be true.

In most beginner scenarios, however, the standard pattern is:

```sql
ON A.PrimaryKey = B.ForeignKey
```

---

# 40. Primary Key and Foreign Key

JOINs commonly connect:

```text
Primary Key
      ↓
Foreign Key
```

For example:

### Customers

```text
CustomerID = Primary Key
```

### Orders

```text
CustomerID = Foreign Key
```

Relationship:

```text
Customers.CustomerID
          =
Orders.CustomerID
```

This is the foundation of the JOIN.

---

# 41. Primary Key Example

```text
Customers
-------------------------
CustomerID  CustomerName
1           Alfreds
2           Ana
3           Antonio
```

Here:

```text
CustomerID
```

uniquely identifies a customer.

So:

```text
CustomerID = Primary Key
```

---

# 42. Foreign Key Example

```text
Orders
------------------------------
OrderID  CustomerID  OrderDate
10308    2           1996-09-18
10365    3           1996-11-27
```

Here:

```text
CustomerID
```

points to a customer.

Therefore:

```text
Orders.CustomerID
```

is a foreign key referencing:

```text
Customers.CustomerID
```

---

# 43. JOIN Relationship Diagram

```text
+----------------------+
|      Customers       |
+----------------------+
| PK CustomerID        |
| CustomerName         |
| ContactName          |
| Country              |
+----------+-----------+
           |
           | CustomerID
           |
           ↓
+----------------------+
|        Orders        |
+----------------------+
| PK OrderID           |
| FK CustomerID        |
| FK EmployeeID        |
| OrderDate            |
| FK ShipperID         |
+----------+-----------+
           |
           | OrderID
           |
           ↓
+----------------------+
|    OrderDetails      |
+----------------------+
| FK OrderID           |
| FK ProductID         |
| Quantity             |
+----------+-----------+
           |
           | ProductID
           |
           ↓
+----------------------+
|       Products       |
+----------------------+
| PK ProductID         |
| ProductName          |
| FK SupplierID        |
| FK CategoryID        |
| Price                |
+----------+-----------+
           |
           | CategoryID
           |
           ↓
+----------------------+
|      Categories      |
+----------------------+
| PK CategoryID        |
| CategoryName         |
+----------------------+
```

This diagram represents the relationships that SQL JOINs use.

---

# 44. A Practical Query Using Our Database

Question:

> Show every order with the customer name, product name, and quantity ordered.

We need four tables:

```text
Orders
Customers
OrderDetails
Products
```

Query:

```sql
SELECT O.OrderID,
       C.CustomerName,
       P.ProductName,
       OD.Quantity
FROM Orders AS O
INNER JOIN Customers AS C
ON O.CustomerID = C.CustomerID
INNER JOIN OrderDetails AS OD
ON O.OrderID = OD.OrderID
INNER JOIN Products AS P
ON OD.ProductID = P.ProductID;
```

This is a practical example of why JOINs are powerful.

---

# 45. Another Practical Query

Question:

> Show each product and its category and supplier.

Tables required:

```text
Products
Categories
Suppliers
```

Relationships:

```text
Products.CategoryID → Categories.CategoryID

Products.SupplierID → Suppliers.SupplierID
```

Query:

```sql
SELECT P.ProductID,
       P.ProductName,
       C.CategoryName,
       S.SupplierName
FROM Products AS P
INNER JOIN Categories AS C
ON P.CategoryID = C.CategoryID
INNER JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID;
```

Result conceptually:

| ProductID | ProductName   | CategoryName | SupplierName   |
| --------: | ------------- | ------------ | -------------- |
|         1 | Chai          | Beverages    | Exotic Liquids |
|         2 | Chang         | Beverages    | Exotic Liquids |
|         3 | Aniseed Syrup | Condiments   | Exotic Liquids |

---

# 46. Another Practical Query

Question:

> Show each order with customer, employee, and shipper information.

Tables:

```text
Orders
Customers
Employees
Shippers
```

Query:

```sql
SELECT O.OrderID,
       O.OrderDate,
       C.CustomerName,
       E.FirstName,
       E.LastName,
       S.ShipperName
FROM Orders AS O
INNER JOIN Customers AS C
ON O.CustomerID = C.CustomerID
INNER JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
INNER JOIN Shippers AS S
ON O.ShipperID = S.ShipperID;
```

This combines four related tables.

---

# 47. How to Decide Which Tables to JOIN

When given a SQL question, follow this process.

## Step 1 — Understand the required output

Example:

> Show OrderID, CustomerName and ShipperName.

Required columns:

```text
OrderID
CustomerName
ShipperName
```

---

## Step 2 — Find where each column exists

```text
OrderID       → Orders
CustomerName  → Customers
ShipperName   → Shippers
```

Therefore we need:

```text
Orders
Customers
Shippers
```

---

## Step 3 — Find the relationships

```text
Orders.CustomerID = Customers.CustomerID

Orders.ShipperID = Shippers.ShipperID
```

---

## Step 4 — Write the JOIN

```sql
FROM Orders AS O
INNER JOIN Customers AS C
ON O.CustomerID = C.CustomerID
INNER JOIN Shippers AS S
ON O.ShipperID = S.ShipperID
```

---

## Step 5 — Select the required columns

```sql
SELECT O.OrderID,
       C.CustomerName,
       S.ShipperName
```

Complete query:

```sql
SELECT O.OrderID,
       C.CustomerName,
       S.ShipperName
FROM Orders AS O
INNER JOIN Customers AS C
ON O.CustomerID = C.CustomerID
INNER JOIN Shippers AS S
ON O.ShipperID = S.ShipperID;
```

---

# 48. A Simple JOIN Thinking Method

Whenever you see a JOIN question, think:

```text
WHAT do I need?
      ↓
WHERE is each column?
      ↓
WHICH tables are required?
      ↓
HOW are those tables related?
      ↓
WRITE JOIN
      ↓
FILTER if necessary
      ↓
SORT if necessary
```

---

# 49. INNER JOIN Mental Model

Think of:

```text
Table A
```

and:

```text
Table B
```

as two sets.

```text
        TABLE A             TABLE B

      +---------+         +---------+
      |         |         |         |
      |    A    |         |    B    |
      |         |         |         |
      |     +---+---------+---+     |
      |     |   MATCHING   |       |
      |     +---------------+       |
      |                             |
      +-----------------------------+
```

INNER JOIN returns only:

```text
MATCHING
```

---

# 50. INNER JOIN in One Sentence

> **INNER JOIN combines related tables and returns only rows where the JOIN condition matches in both tables.**

---

# 51. Most Important Syntax to Remember

Basic:

```sql
SELECT ...
FROM TableA
INNER JOIN TableB
ON TableA.Key = TableB.Key;
```

With aliases:

```sql
SELECT A.Column1,
       B.Column2
FROM TableA AS A
INNER JOIN TableB AS B
ON A.Key = B.Key;
```

Multiple tables:

```sql
SELECT ...
FROM TableA AS A
INNER JOIN TableB AS B
ON A.Key = B.Key
INNER JOIN TableC AS C
ON B.Key = C.Key;
```

With filtering:

```sql
SELECT ...
FROM TableA AS A
INNER JOIN TableB AS B
ON A.Key = B.Key
WHERE A.Column > 100;
```

With sorting:

```sql
SELECT ...
FROM TableA AS A
INNER JOIN TableB AS B
ON A.Key = B.Key
ORDER BY A.Column DESC;
```

---

# 52. INNER JOIN — Quick Reference

| Concept      | Meaning                        |
| ------------ | ------------------------------ |
| `JOIN`       | Same as `INNER JOIN`           |
| `INNER JOIN` | Returns matching rows          |
| `ON`         | Defines how tables are related |
| Primary Key  | Uniquely identifies a row      |
| Foreign Key  | References another table's key |
| Alias        | Short name for a table         |
| `WHERE`      | Filters joined results         |
| `ORDER BY`   | Sorts results                  |

---

# 53. Common Mistakes

## Mistake 1 — Forgetting the ON condition

Incorrect:

```sql
SELECT *
FROM Products
INNER JOIN Categories;
```

Correct:

```sql
SELECT *
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

---

## Mistake 2 — Joining unrelated columns

Incorrect:

```sql
ON Products.ProductID = Categories.CategoryID
```

The relationship should normally be:

```sql
ON Products.CategoryID = Categories.CategoryID
```

Always identify the actual relationship between the tables.

---

## Mistake 3 — Ambiguous columns

Avoid:

```sql
SELECT CategoryID
```

when both tables contain `CategoryID`.

Prefer:

```sql
SELECT Products.CategoryID
```

or:

```sql
SELECT P.CategoryID
```

---

## Mistake 4 — Forgetting that rows can multiply

Joining:

```text
Customers → Orders
```

can produce multiple rows for the same customer because one customer may have many orders.

This is expected behavior.

---

## Mistake 5 — Thinking JOIN permanently combines tables

A JOIN does **not** permanently merge the tables.

It creates a combined **result set for that query**.

The original tables remain separate.

---

# 54. INNER JOIN vs Database Design

Database design:

```text
Customers
    ↓
Orders
    ↓
OrderDetails
    ↓
Products
    ↓
Categories
```

Data is stored separately.

JOIN:

```text
Customers
    +
Orders
    +
OrderDetails
    +
Products
    +
Categories
```

allows us to retrieve the information together when required.

Therefore:

> **Normalization separates data; JOINs bring related data together when needed.**

---

# 55. Real-World Example

Imagine an online shopping system.

The database stores:

```text
Customer
    ↓
Order
    ↓
Order Items
    ↓
Product
    ↓
Category
```

When the customer opens an order page, the application may need:

```text
Customer Name
Order Date
Product Name
Category
Quantity
Price
```

Those values may exist in five different tables.

SQL can bring them together:

```sql
SELECT C.CustomerName,
       O.OrderDate,
       P.ProductName,
       CAT.CategoryName,
       OD.Quantity,
       P.Price
FROM Customers AS C
INNER JOIN Orders AS O
ON C.CustomerID = O.CustomerID
INNER JOIN OrderDetails AS OD
ON O.OrderID = OD.OrderID
INNER JOIN Products AS P
ON OD.ProductID = P.ProductID
INNER JOIN Categories AS CAT
ON P.CategoryID = CAT.CategoryID;
```

This is the real power of relational databases.

---

# 56. Final INNER JOIN Formula

Remember this pattern:

```text
SELECT
    columns
FROM
    first_table
INNER JOIN
    second_table
ON
    related_column = related_column;
```

For our database:

```text
Orders.CustomerID
        =
Customers.CustomerID
```

```text
Orders.OrderID
        =
OrderDetails.OrderID
```

```text
OrderDetails.ProductID
        =
Products.ProductID
```

```text
Products.CategoryID
        =
Categories.CategoryID
```

These relationships allow us to travel through the database and retrieve related information.

---

# 57. Final Summary

### INNER JOIN

```sql
INNER JOIN
```

means:

> **Return only records where a matching value exists in both tables.**

### Basic syntax

```sql
SELECT ...
FROM TableA
INNER JOIN TableB
ON TableA.Key = TableB.Key;
```

### Short form

```sql
JOIN
```

is equivalent to:

```sql
INNER JOIN
```

### Key concepts

```text
Primary Key
     ↓
Foreign Key
     ↓
JOIN condition
     ↓
Matching rows
     ↓
Combined result
```

### Our Northwind database

```text
Customers (91)
      |
      | CustomerID
      ↓
Orders (196)
      |
      | OrderID
      ↓
OrderDetails (518)
      |
      | ProductID
      ↓
Products (77)
      |
      | CategoryID
      ↓
Categories (8)
```

Additional relationships:

```text
Orders → Employees
Orders → Shippers
Products → Suppliers
```

The key idea to remember is:

> **Tables store related data separately. INNER JOIN connects those tables through related keys and returns only the matching records.**
