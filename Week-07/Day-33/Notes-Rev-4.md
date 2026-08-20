# RDBMS Normalization with Python + MySQL
## 1NF → 2NF → 3NF + Two Related Tables + Python CRUD + JOIN Operations

---

# 1. Objective

In this example we will learn how to take a large customer/order dataset and design a proper **Relational Database Management System (RDBMS)**.

We will cover:

1. What is RDBMS?
2. Rules for splitting data into tables
3. 1NF — First Normal Form
4. 2NF — Second Normal Form
5. 3NF — Third Normal Form
6. Designing two related tables
7. Primary Key
8. Foreign Key
9. CSV data
10. Creating tables using Python
11. Reading CSV using Python
12. Inserting multiple records
13. SELECT
14. WHERE
15. ORDER BY
16. JOIN
17. INNER JOIN
18. LEFT JOIN
19. Five SQL practice questions
20. Complete Python modular program

---

# 2. Example Business Requirement

Suppose we have a company that maintains customer orders.

Initially, somebody stores everything in one table:

| CustomerID | CustomerName | City | Country | OrderID | Product | Quantity | Price |
|---:|---|---|---|---:|---|---:|---:|
| 1 | Alfreds Futterkiste | Berlin | Germany | 101 | Chai | 2 | 18 |
| 1 | Alfreds Futterkiste | Berlin | Germany | 102 | Chang | 3 | 19 |
| 2 | Ana Trujillo Emparedados | Mexico D.F. | Mexico | 103 | Chai | 1 | 18 |
| 3 | Antonio Moreno Taquería | Mexico D.F. | Mexico | 104 | Aniseed Syrup | 4 | 10 |
| 4 | Around the Horn | London | UK | 105 | Chang | 2 | 19 |

This works initially.

But there is a problem.

Customer information is repeated.

For example:

```text
CustomerID = 1

Alfreds Futterkiste
Berlin
Germany
```

appears multiple times.

This causes:

- Duplicate data
- Update problems
- Insert problems
- Delete problems
- More storage
- Difficult maintenance

Therefore, we normalize the database.

---

# 3. What is Normalization?

Normalization is the process of organizing data into related tables so that:

```text
Duplicate data is reduced
        ↓
Data consistency improves
        ↓
Tables become easier to maintain
        ↓
Relationships are clearly defined
```

The commonly discussed normal forms are:

```text
1NF
 ↓
2NF
 ↓
3NF
```

For our beginner RDBMS example, we will mainly focus on **1NF, 2NF and 3NF**.

---

# 4. Rules for Splitting Data into Tables

When designing tables, ask these questions:

### Rule 1 — What is the entity?

Example:

```text
Customer
Order
Product
Department
Student
Employee
```

Each important entity usually becomes a table.

---

### Rule 2 — What uniquely identifies the record?

For Customer:

```text
CustomerID
```

For Order:

```text
OrderID
```

These become primary keys.

---

### Rule 3 — Does the column belong to the entity?

Customer table:

```text
CustomerID
CustomerName
ContactName
City
Country
```

These describe the customer.

Order table:

```text
OrderID
CustomerID
Product
Quantity
Price
```

These describe an order.

---

### Rule 4 — Avoid repeating the same information

Bad:

```text
OrderID | CustomerID | CustomerName | City | Country
```

If a customer places 20 orders, the customer information is repeated 20 times.

Better:

```text
Customer
---------
CustomerID
CustomerName
City
Country
```

and:

```text
Orders
------
OrderID
CustomerID
Product
Quantity
Price
```

---

### Rule 5 — Use a Primary Key

Every table should normally have a column that uniquely identifies each row.

Example:

```sql
CustomerID INT PRIMARY KEY
```

---

### Rule 6 — Use Foreign Keys for relationships

The Orders table needs to know which customer placed the order.

Therefore:

```text
Orders.CustomerID
        ↓
Customers.CustomerID
```

`Orders.CustomerID` becomes a foreign key.

---

# 5. Starting Dataset

We will use the customer information from the provided customer table.

For this demonstration we only need **10 customers**.

---

# 6. Customer Data

| CustomerID | CustomerName | ContactName | Address | City | PostalCode | Country |
|---:|---|---|---|---|---|---|
| 1 | Alfreds Futterkiste | Maria Anders | Obere Str. 57 | Berlin | 12209 | Germany |
| 2 | Ana Trujillo Emparedados | Ana Trujillo | Avda. Constitución 2222 | México D.F. | 05021 | Mexico |
| 3 | Antonio Moreno Taquería | Antonio Moreno | Mataderos 2312 | México D.F. | 05023 | Mexico |
| 4 | Around the Horn | Thomas Hardy | 120 Hanover Sq. | London | WA1 1DP | UK |
| 5 | Berglunds snabbköp | Christina Berglund | Berguvsvägen 8 | Luleå | S-958 22 | Sweden |
| 6 | Blauer See Delikatessen | Hanna Moos | Forsterstr. 57 | Mannheim | 68306 | Germany |
| 7 | Blondel père et fils | Frédérique Citeaux | 24, place Kléber | Strasbourg | 67000 | France |
| 8 | Bólido Comidas preparadas | Martín Sommer | C/ Araquil, 67 | Madrid | 28023 | Spain |
| 9 | Bon app' | Laurence Lebihans | 12, rue des Bouchers | Marseille | 13008 | France |
| 10 | Bottom-Dollar Market | Elizabeth Lincoln | 23 Tsawassen Blvd. | Tsawassen | T2F 8M4 | Canada |

---

# 7. Example Order Data

Now suppose these customers place orders.

We create another table:

| OrderID | CustomerID | Product | Quantity | Price |
|---:|---:|---|---:|---:|
| 101 | 1 | Chai | 2 | 18.00 |
| 102 | 1 | Chang | 3 | 19.00 |
| 103 | 2 | Chai | 1 | 18.00 |
| 104 | 2 | Aniseed Syrup | 4 | 10.00 |
| 105 | 3 | Chang | 2 | 19.00 |
| 106 | 4 | Chai | 5 | 18.00 |
| 107 | 5 | Chef Anton's Cajun Seasoning | 2 | 22.00 |
| 108 | 6 | Chai | 3 | 18.00 |
| 109 | 8 | Chang | 1 | 19.00 |
| 110 | 10 | Aniseed Syrup | 6 | 10.00 |

Notice:

```text
CustomerID
```

exists in both tables.

But its purpose is different.

In:

```text
Customers
```

it is the:

```text
PRIMARY KEY
```

In:

```text
Orders
```

it is the:

```text
FOREIGN KEY
```

---

# 8. Relationship

The relationship is:

```text
Customers
    |
    | CustomerID
    |
    | 1
    |
    |------< Many
              |
            Orders
```

Meaning:

```text
One Customer
     ↓
Can have
     ↓
Many Orders
```

This is called a:

```text
ONE-TO-MANY relationship
```

---

# 9. 1NF — First Normal Form

## Rule

A table is in 1NF when:

1. Each column contains atomic values.
2. There are no repeating groups.
3. Each row represents one record.
4. Each column represents one attribute.

---

# 10. Bad Example — Not 1NF

Suppose we store:

| CustomerID | CustomerName | Products |
|---:|---|---|
| 1 | Alfreds Futterkiste | Chai, Chang |
| 2 | Ana Trujillo | Chai, Aniseed Syrup |

The `Products` column contains multiple values:

```text
Chai, Chang
```

This violates the idea of atomic values.

---

# 11. Convert to 1NF

Instead:

| CustomerID | CustomerName | Product |
|---:|---|---|
| 1 | Alfreds Futterkiste | Chai |
| 1 | Alfreds Futterkiste | Chang |
| 2 | Ana Trujillo | Chai |
| 2 | Ana Trujillo | Aniseed Syrup |

Each cell contains one value.

Now the data is atomic.

---

# 12. 2NF — Second Normal Form

2NF requires:

```text
1NF
+
No partial dependency on a composite key
```

A simple way to understand this:

If a table has a composite primary key:

```text
PRIMARY KEY (CustomerID, ProductID)
```

every non-key column should depend on the complete key.

---

# 13. Example of Partial Dependency

Suppose we create:

```text
CustomerOrder
```

with:

```text
CustomerID
ProductID
CustomerName
ProductName
Quantity
```

and:

```text
PRIMARY KEY(CustomerID, ProductID)
```

Problem:

```text
CustomerName
```

depends only on:

```text
CustomerID
```

not:

```text
CustomerID + ProductID
```

Similarly:

```text
ProductName
```

depends only on:

```text
ProductID
```

Therefore, the table has partial dependencies.

---

# 14. Move Towards 2NF

Separate the entities.

### Customers

```text
CustomerID
CustomerName
ContactName
Address
City
PostalCode
Country
```

### Products

```text
ProductID
ProductName
Price
```

### Orders

```text
OrderID
CustomerID
ProductID
Quantity
```

Now each entity has its own information.

---

# 15. 3NF — Third Normal Form

3NF requires:

```text
2NF
+
No transitive dependency
```

In simple terms:

A non-key column should depend on:

```text
the key
```

and not on another non-key column.

---

# 16. Example of Transitive Dependency

Suppose we have:

```text
CustomerID
CustomerName
City
Country
CountryCode
```

If:

```text
CustomerID → City
City → Country
```

then:

```text
CustomerID → City → Country
```

There is an indirect dependency.

For a proper design, country information can be separated if the business requirements justify it.

---

# 17. Our Final Beginner-Friendly 3NF Design

For this lesson we will keep the design simple with two tables:

```text
Customers
Orders
```

## Customers

```text
CustomerID       PRIMARY KEY
CustomerName
ContactName
Address
City
PostalCode
Country
```

## Orders

```text
OrderID          PRIMARY KEY
CustomerID       FOREIGN KEY
Product
Quantity
Price
```

This is enough to demonstrate:

```text
Primary Key
Foreign Key
One-to-Many
INSERT
SELECT
WHERE
ORDER BY
JOIN
```

---

# 18. Database Schema

```text
+---------------------------+
|        Customers          |
+---------------------------+
| PK CustomerID             |
|    CustomerName           |
|    ContactName            |
|    Address                |
|    City                   |
|    PostalCode             |
|    Country                |
+-------------+-------------+
              |
              |
              | 1
              |
              | CustomerID
              |
              | Many
+-------------v-------------+
|          Orders           |
+---------------------------+
| PK OrderID                |
| FK CustomerID             |
|    Product                |
|    Quantity               |
|    Price                  |
+---------------------------+
```

---

# 19. SQL — Create Database

```sql
CREATE DATABASE training_db;
```

Use the database:

```sql
USE training_db;
```

---

# 20. SQL — Create Customers Table

```sql
CREATE TABLE IF NOT EXISTS Customers(
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    ContactName VARCHAR(100),
    Address VARCHAR(150),
    City VARCHAR(50),
    PostalCode VARCHAR(20),
    Country VARCHAR(50)
);
```

---

# 21. SQL — Create Orders Table

```sql
CREATE TABLE IF NOT EXISTS Orders(
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    Product VARCHAR(100),
    Quantity INT,
    Price DECIMAL(10,2),

    FOREIGN KEY(CustomerID)
    REFERENCES Customers(CustomerID)
);
```

---

# 22. Important Rule — Create Parent First

Because:

```text
Orders.CustomerID
```

references:

```text
Customers.CustomerID
```

we should create:

```text
Customers
```

first.

Then:

```text
Orders
```

Therefore:

```text
Customers
    ↓
Orders
```

---

# 23. CSV File — customers.csv

Save the following data as:

```text
customers.csv
```

```csv
CustomerID,CustomerName,ContactName,Address,City,PostalCode,Country
1,"Alfreds Futterkiste","Maria Anders","Obere Str. 57","Berlin","12209","Germany"
2,"Ana Trujillo Emparedados","Ana Trujillo","Avda. Constitución 2222","México D.F.","05021","Mexico"
3,"Antonio Moreno Taquería","Antonio Moreno","Mataderos 2312","México D.F.","05023","Mexico"
4,"Around the Horn","Thomas Hardy","120 Hanover Sq.","London","WA1 1DP","UK"
5,"Berglunds snabbköp","Christina Berglund","Berguvsvägen 8","Luleå","S-958 22","Sweden"
6,"Blauer See Delikatessen","Hanna Moos","Forsterstr. 57","Mannheim","68306","Germany"
7,"Blondel père et fils","Frédérique Citeaux","24, place Kléber","Strasbourg","67000","France"
8,"Bólido Comidas preparadas","Martín Sommer","C/ Araquil, 67","Madrid","28023","Spain"
9,"Bon app'","Laurence Lebihans","12, rue des Bouchers","Marseille","13008","France"
10,"Bottom-Dollar Market","Elizabeth Lincoln","23 Tsawassen Blvd.","Tsawassen","T2F 8M4","Canada"
```

---

# 24. CSV File — orders.csv

Save the following as:

```text
orders.csv
```

```csv
OrderID,CustomerID,Product,Quantity,Price
101,1,"Chai",2,18.00
102,1,"Chang",3,19.00
103,2,"Chai",1,18.00
104,2,"Aniseed Syrup",4,10.00
105,3,"Chang",2,19.00
106,4,"Chai",5,18.00
107,5,"Chef Anton's Cajun Seasoning",2,22.00
108,6,"Chai",3,18.00
109,8,"Chang",1,19.00
110,10,"Aniseed Syrup",6,10.00
```

---

# 25. Python Project Structure

We will use modular Python programming.

```text
rdbms_demo/
│
├── database.py
├── create_tables.py
├── insert_customers.py
├── insert_orders.py
├── select_records.py
├── where_records.py
├── order_records.py
├── join_records.py
├── main.py
│
├── customers.csv
└── orders.csv
```

---

# 26. database.py

This module is responsible for creating the MySQL connection.

```python
import mysql.connector


def get_connection():

    connection = mysql.connector.connect(
        host="localhost",
        user="root",
        password="your_password",
        database="training_db"
    )

    return connection
```

---

# 27. create_tables.py

```python
from database import get_connection


def create_customers_table():

    connection = get_connection()
    cursor = connection.cursor()

    sql = """
    CREATE TABLE IF NOT EXISTS Customers(
        CustomerID INT PRIMARY KEY,
        CustomerName VARCHAR(100),
        ContactName VARCHAR(100),
        Address VARCHAR(150),
        City VARCHAR(50),
        PostalCode VARCHAR(20),
        Country VARCHAR(50)
    )
    """

    cursor.execute(sql)

    connection.commit()

    cursor.close()
    connection.close()

    print("Customers table created successfully.")


def create_orders_table():

    connection = get_connection()
    cursor = connection.cursor()

    sql = """
    CREATE TABLE IF NOT EXISTS Orders(
        OrderID INT PRIMARY KEY,
        CustomerID INT,
        Product VARCHAR(100),
        Quantity INT,
        Price DECIMAL(10,2),

        FOREIGN KEY(CustomerID)
        REFERENCES Customers(CustomerID)
    )
    """

    cursor.execute(sql)

    connection.commit()

    cursor.close()
    connection.close()

    print("Orders table created successfully.")


def main():

    create_customers_table()
    create_orders_table()


if __name__ == "__main__":
    main()
```

---

# 28. insert_customers.py

Read the CSV file and insert multiple records.

```python
import csv

from database import get_connection


def read_customers_from_csv(filename):

    customers = []

    with open(filename, mode="r", encoding="utf-8") as file:

        reader = csv.reader(file)

        next(reader)

        for row in reader:

            customer = (
                int(row[0]),
                row[1],
                row[2],
                row[3],
                row[4],
                row[5],
                row[6]
            )

            customers.append(customer)

    return customers


def insert_customers():

    customers = read_customers_from_csv("customers.csv")

    connection = get_connection()
    cursor = connection.cursor()

    sql = """
    INSERT INTO Customers(
        CustomerID,
        CustomerName,
        ContactName,
        Address,
        City,
        PostalCode,
        Country
    )
    VALUES(%s, %s, %s, %s, %s, %s, %s)
    """

    cursor.executemany(sql, customers)

    connection.commit()

    print(len(customers), "customers inserted successfully.")

    cursor.close()
    connection.close()


def main():

    insert_customers()


if __name__ == "__main__":
    main()
```

---

# 29. insert_orders.py

Read orders from CSV and insert multiple records.

```python
import csv

from database import get_connection


def read_orders_from_csv(filename):

    orders = []

    with open(filename, mode="r", encoding="utf-8") as file:

        reader = csv.reader(file)

        next(reader)

        for row in reader:

            order = (
                int(row[0]),
                int(row[1]),
                row[2],
                int(row[3]),
                float(row[4])
            )

            orders.append(order)

    return orders


def insert_orders():

    orders = read_orders_from_csv("orders.csv")

    connection = get_connection()
    cursor = connection.cursor()

    sql = """
    INSERT INTO Orders(
        OrderID,
        CustomerID,
        Product,
        Quantity,
        Price
    )
    VALUES(%s, %s, %s, %s, %s)
    """

    cursor.executemany(sql, orders)

    connection.commit()

    print(len(orders), "orders inserted successfully.")

    cursor.close()
    connection.close()


def main():

    insert_orders()


if __name__ == "__main__":
    main()
```

---

# 30. Why Use executemany()?

Instead of:

```python
cursor.execute(...)
cursor.execute(...)
cursor.execute(...)
cursor.execute(...)
```

we can use:

```python
cursor.executemany(sql, records)
```

Example:

```python
students = [
    ("Alex", "CSE", 91),
    ("John", "ECE", 88),
    ("Priya", "CSE", 95)
]

cursor.executemany(sql, students)
```

This is useful when inserting multiple CSV records.

---

# 31. Select All Customers

Create:

```text
select_records.py
```

```python
from database import get_connection


def select_customers():

    connection = get_connection()
    cursor = connection.cursor()

    cursor.execute("""
        SELECT *
        FROM Customers
    """)

    rows = cursor.fetchall()

    print("Customer Records")
    print("------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    select_customers()


if __name__ == "__main__":
    main()
```

---

# 32. Select All Orders

```python
from database import get_connection


def select_orders():

    connection = get_connection()
    cursor = connection.cursor()

    cursor.execute("""
        SELECT *
        FROM Orders
    """)

    rows = cursor.fetchall()

    print("Order Records")
    print("------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    select_orders()


if __name__ == "__main__":
    main()
```

---

# 33. WHERE Example

Find all customers from Germany.

```python
from database import get_connection


def find_german_customers():

    connection = get_connection()
    cursor = connection.cursor()

    sql = """
    SELECT *
    FROM Customers
    WHERE Country = %s
    """

    value = ("Germany",)

    cursor.execute(sql, value)

    rows = cursor.fetchall()

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    find_german_customers()


if __name__ == "__main__":
    main()
```

---

# 34. ORDER BY Example

Find customers sorted by name.

```python
from database import get_connection


def order_customers():

    connection = get_connection()
    cursor = connection.cursor()

    cursor.execute("""
        SELECT *
        FROM Customers
        ORDER BY CustomerName ASC
    """)

    rows = cursor.fetchall()

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    order_customers()


if __name__ == "__main__":
    main()
```

---

# 35. INNER JOIN

Now we reach the most important part.

We have:

```text
Customers
```

and:

```text
Orders
```

We want to see:

```text
CustomerName
Country
OrderID
Product
Quantity
Price
```

The information is stored in two different tables.

Therefore we use:

```sql
JOIN
```

---

# 36. INNER JOIN SQL

```sql
SELECT
    Customers.CustomerID,
    Customers.CustomerName,
    Customers.Country,
    Orders.OrderID,
    Orders.Product,
    Orders.Quantity,
    Orders.Price
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

# 37. INNER JOIN Concept

```text
Customers.CustomerID
          =
Orders.CustomerID
```

Example:

```text
Customers
CustomerID = 1
CustomerName = Alfreds Futterkiste

        JOIN

Orders
CustomerID = 1
OrderID = 101
Product = Chai
```

Result:

```text
Alfreds Futterkiste | 101 | Chai
```

---

# 38. Python INNER JOIN

Create:

```text
join_records.py
```

```python
from database import get_connection


def customer_orders():

    connection = get_connection()
    cursor = connection.cursor()

    sql = """
    SELECT
        Customers.CustomerID,
        Customers.CustomerName,
        Customers.Country,
        Orders.OrderID,
        Orders.Product,
        Orders.Quantity,
        Orders.Price
    FROM Customers
    INNER JOIN Orders
        ON Customers.CustomerID = Orders.CustomerID
    ORDER BY Customers.CustomerID
    """

    cursor.execute(sql)

    rows = cursor.fetchall()

    print("Customer Orders")
    print("=" * 80)

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    customer_orders()


if __name__ == "__main__":
    main()
```

---

# 39. Expected JOIN Result

Conceptually:

| CustomerID | CustomerName | Country | OrderID | Product | Quantity | Price |
|---:|---|---|---:|---|---:|---:|
| 1 | Alfreds Futterkiste | Germany | 101 | Chai | 2 | 18 |
| 1 | Alfreds Futterkiste | Germany | 102 | Chang | 3 | 19 |
| 2 | Ana Trujillo Emparedados | Mexico | 103 | Chai | 1 | 18 |
| 2 | Ana Trujillo Emparedados | Mexico | 104 | Aniseed Syrup | 4 | 10 |
| 3 | Antonio Moreno Taquería | Mexico | 105 | Chang | 2 | 19 |
| 4 | Around the Horn | UK | 106 | Chai | 5 | 18 |
| 5 | Berglunds snabbköp | Sweden | 107 | Chef Anton's Cajun Seasoning | 2 | 22 |
| 6 | Blauer See Delikatessen | Germany | 108 | Chai | 3 | 18 |
| 8 | Bólido Comidas preparadas | Spain | 109 | Chang | 1 | 19 |
| 10 | Bottom-Dollar Market | Canada | 110 | Aniseed Syrup | 6 | 10 |

Notice:

```text
CustomerID 7
CustomerID 9
```

do not appear in the INNER JOIN result because they currently have no orders.

---

# 40. LEFT JOIN

If we want to display:

```text
ALL customers
```

including customers who have no orders, use:

```sql
LEFT JOIN
```

SQL:

```sql
SELECT
    Customers.CustomerID,
    Customers.CustomerName,
    Orders.OrderID,
    Orders.Product
FROM Customers
LEFT JOIN Orders
    ON Customers.CustomerID = Orders.CustomerID;
```

Customer 7 and Customer 9 will also appear.

Their order columns will contain:

```text
NULL
```

---

# 41. INNER JOIN vs LEFT JOIN

| JOIN | Meaning |
|---|---|
| INNER JOIN | Matching records from both tables |
| LEFT JOIN | All records from left table + matching records from right table |
| RIGHT JOIN | All records from right table + matching records from left table |
| CROSS JOIN | Every row combined with every row |

For beginners, focus first on:

```text
INNER JOIN
LEFT JOIN
```

---

# 42. JOIN with WHERE

Find all orders placed by customers from Germany.

```sql
SELECT
    Customers.CustomerName,
    Customers.Country,
    Orders.OrderID,
    Orders.Product,
    Orders.Quantity
FROM Customers
INNER JOIN Orders
    ON Customers.CustomerID = Orders.CustomerID
WHERE Customers.Country = 'Germany';
```

---

# 43. JOIN with ORDER BY

Sort orders by quantity.

```sql
SELECT
    Customers.CustomerName,
    Orders.Product,
    Orders.Quantity,
    Orders.Price
FROM Customers
INNER JOIN Orders
    ON Customers.CustomerID = Orders.CustomerID
ORDER BY Orders.Quantity DESC;
```

---

# 44. Calculated Column

We can calculate total order value.

```sql
SELECT
    Customers.CustomerName,
    Orders.Product,
    Orders.Quantity,
    Orders.Price,
    Orders.Quantity * Orders.Price AS Total
FROM Customers
INNER JOIN Orders
    ON Customers.CustomerID = Orders.CustomerID;
```

Example:

```text
Quantity = 3
Price = 19

Total = 3 × 19

Total = 57
```

---

# 45. Python — JOIN with Calculated Total

```python
from database import get_connection


def order_details():

    connection = get_connection()
    cursor = connection.cursor()

    sql = """
    SELECT
        Customers.CustomerName,
        Customers.Country,
        Orders.Product,
        Orders.Quantity,
        Orders.Price,
        Orders.Quantity * Orders.Price AS Total
    FROM Customers
    INNER JOIN Orders
        ON Customers.CustomerID = Orders.CustomerID
    ORDER BY Total DESC
    """

    cursor.execute(sql)

    rows = cursor.fetchall()

    print("Order Details")
    print("=" * 100)

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    order_details()


if __name__ == "__main__":
    main()
```

---

# 46. Main Program

We can create:

```text
main.py
```

```python
from create_tables import main as create_tables
from insert_customers import insert_customers
from insert_orders import insert_orders
from join_records import customer_orders


def main():

    print("Creating tables...")
    create_tables()

    print("\nInserting customers...")
    insert_customers()

    print("\nInserting orders...")
    insert_orders()

    print("\nDisplaying customer orders...")
    customer_orders()


if __name__ == "__main__":
    main()
```

---

# 47. Execution Flow

The complete Python application works like this:

```text
main.py
   |
   +---- create_tables.py
   |
   +---- customers.csv
   |          |
   |          ↓
   |    insert_customers.py
   |
   +---- orders.csv
   |          |
   |          ↓
   |    insert_orders.py
   |
   ↓
MySQL Database
   |
   +---- Customers
   |
   +---- Orders
   |
   ↓
join_records.py
   |
   ↓
INNER JOIN
   |
   ↓
Output
```

---

# 48. Complete Database Flow

```text
CSV
 ↓
Python csv module
 ↓
List of tuples
 ↓
executemany()
 ↓
MySQL
 ↓
Customers Table
Orders Table
 ↓
JOIN
 ↓
Python fetchall()
 ↓
Display Result
```

---

# 49. Important Python Concepts Used

This example teaches several Python concepts together.

| Python Concept | Where Used |
|---|---|
| Function | Every operation |
| Module | Separate `.py` files |
| Import | `from database import get_connection` |
| List | Store CSV records |
| Tuple | Database record |
| File handling | Reading CSV |
| `csv.reader()` | CSV processing |
| Loop | Reading records |
| Exception handling | Can be added later |
| MySQL connector | Database communication |
| `execute()` | Single SQL operation |
| `executemany()` | Multiple records |
| `fetchall()` | Read multiple records |

---

# 50. Important SQL Concepts Used

| SQL Concept | Example |
|---|---|
| CREATE DATABASE | Create database |
| CREATE TABLE | Create tables |
| PRIMARY KEY | CustomerID |
| FOREIGN KEY | Orders.CustomerID |
| INSERT | Add records |
| SELECT | Read records |
| WHERE | Filter records |
| ORDER BY | Sort records |
| INNER JOIN | Combine related tables |
| LEFT JOIN | Keep all customers |
| AS | Column alias |
| Arithmetic | Quantity × Price |

---

# 51. Why Did We Split the Table?

Original design:

```text
CustomerID
CustomerName
City
Country
OrderID
Product
Quantity
Price
```

Everything is together.

Problem:

```text
Customer information
        +
Order information
```

are two different concepts.

Therefore:

```text
Customers
        +
Orders
```

---

# 52. Dependency

Customer table:

```text
CustomerID
     ↓
CustomerName
ContactName
Address
City
PostalCode
Country
```

Order table:

```text
OrderID
   ↓
CustomerID
Product
Quantity
Price
```

Relationship:

```text
Customers.CustomerID
        ↓
Orders.CustomerID
```

---

# 53. Primary Key

Definition:

> A primary key uniquely identifies each record in a table.

Customers:

```sql
CustomerID INT PRIMARY KEY
```

Orders:

```sql
OrderID INT PRIMARY KEY
```

Example:

```text
CustomerID
1
2
3
4
5
```

No two customers should have the same CustomerID.

---

# 54. Foreign Key

Definition:

> A foreign key is a column that references a key in another table.

Orders:

```sql
CustomerID INT
```

references:

```sql
Customers(CustomerID)
```

Therefore:

```text
Customers
CustomerID = 1
        ↑
        |
        |
Orders
CustomerID = 1
```

---

# 55. Referential Integrity

The foreign key prevents invalid relationships.

Suppose:

```text
Customers
```

contains:

```text
CustomerID = 1
```

Then an order can contain:

```text
CustomerID = 1
```

But if there is no:

```text
CustomerID = 999
```

in Customers, an order referencing 999 should not normally be allowed.

This is called:

```text
Referential Integrity
```

---

# 56. 1NF → 2NF → 3NF Summary

```text
RAW DATA
   ↓
Remove repeating groups
   ↓
1NF
   ↓
Remove partial dependencies
   ↓
2NF
   ↓
Remove transitive dependencies
   ↓
3NF
```

---

# 57. Simple Way to Remember

### 1NF

```text
One cell = One value
```

### 2NF

```text
Every non-key column
depends on the complete key
```

### 3NF

```text
Non-key columns
should not depend on other non-key columns
```

---

# 58. Five Practice Questions

## Question 1

Write Python code to find all customers from:

```text
Germany
```

Expected SQL:

```sql
SELECT *
FROM Customers
WHERE Country = 'Germany';
```

---

## Question 2

Write a Python program to display all orders sorted by:

```text
Price DESC
```

Expected SQL:

```sql
SELECT *
FROM Orders
ORDER BY Price DESC;
```

---

## Question 3

Using `INNER JOIN`, display:

```text
CustomerName
Product
Quantity
Price
```

Expected SQL:

```sql
SELECT
    Customers.CustomerName,
    Orders.Product,
    Orders.Quantity,
    Orders.Price
FROM Customers
INNER JOIN Orders
    ON Customers.CustomerID = Orders.CustomerID;
```

---

## Question 4

Display all customers, including customers who have not placed any order.

Hint:

```text
LEFT JOIN
```

Expected SQL:

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID,
    Orders.Product
FROM Customers
LEFT JOIN Orders
    ON Customers.CustomerID = Orders.CustomerID;
```

---

## Question 5

Display:

```text
CustomerName
Product
Quantity
Price
Total
```

where:

```text
Total = Quantity × Price
```

Sort the result by Total from highest to lowest.

Expected SQL:

```sql
SELECT
    Customers.CustomerName,
    Orders.Product,
    Orders.Quantity,
    Orders.Price,
    Orders.Quantity * Orders.Price AS Total
FROM Customers
INNER JOIN Orders
    ON Customers.CustomerID = Orders.CustomerID
ORDER BY Total DESC;
```

---

# 59. Final Learning Model

```text
                    RDBMS
                      |
                      ↓
                Identify Entities
                      |
          +-----------+-----------+
          |                       |
          ↓                       ↓
      Customers                 Orders
          |                       |
          ↓                       ↓
   Primary Key                Primary Key
   CustomerID                  OrderID
          |
          ↓
      Foreign Key
          |
          ↓
        Orders
     CustomerID
          |
          ↓
        JOIN
          |
          ↓
   Combined Information
          |
          ↓
     Python Output
```

---

# 60. What We Learned

By completing this example, we have moved from a flat dataset to a relational database.

```text
Flat Data
   ↓
Normalization
   ↓
1NF
   ↓
2NF
   ↓
3NF
   ↓
Customers Table
   +
Orders Table
   ↓
Primary Key
   +
Foreign Key
   ↓
Python CSV Reading
   ↓
executemany()
   ↓
MySQL
   ↓
SELECT
   ↓
WHERE
   ↓
ORDER BY
   ↓
INNER JOIN
   ↓
LEFT JOIN
```

The most important idea is:

> **We split tables based on entities and relationships, not simply because the table is large.**

In this example:

```text
Customer information
        ↓
Customers table

Order information
        ↓
Orders table

Relationship
        ↓
CustomerID

Connection
        ↓
FOREIGN KEY

Combined data
        ↓
JOIN
```

This is the basic foundation for building an RDBMS application using **Python + MySQL**.
