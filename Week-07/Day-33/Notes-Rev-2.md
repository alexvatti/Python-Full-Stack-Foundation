# Day 33 — CSV to MySQL

## Module: Read Customer Data from CSV and Insert Multiple Records

In this demo, customer data is maintained in a **CSV file**.

Python will:

```text
CSV File
   ↓
Read CSV
   ↓
Convert rows into list
   ↓
executemany()
   ↓
MySQL Customers Table
```

We will use the **first 50 customer records** from the given Customer table.

---

# 1. Customer CSV File

Create the following file:

```text
customers.csv
```

The CSV contains the same columns as the MySQL `Customers` table.

```csv
CustomerID,CustomerName,ContactName,Address,City,PostalCode,Country
1,Alfreds Futterkiste,Maria Anders,Obere Str. 57,Berlin,12209,Germany
2,Ana Trujillo Emparedados y helados,Ana Trujillo,Avda. de la Constitución 2222,México D.F.,05021,Mexico
3,Antonio Moreno Taquería,Antonio Moreno,Mataderos 2312,México D.F.,05023,Mexico
4,Around the Horn,Thomas Hardy,120 Hanover Sq.,London,WA1 1DP,UK
5,Berglunds snabbköp,Christina Berglund,Berguvsvägen 8,Luleå,S-958 22,Sweden
6,Blauer See Delikatessen,Hanna Moos,Forsterstr. 57,Mannheim,68306,Germany
7,Blondel père et fils,Frédérique Citeaux,"24, place Kléber",Strasbourg,67000,France
8,Bólido Comidas preparadas,Martín Sommer,"C/ Araquil, 67",Madrid,28023,Spain
9,Bon app',Laurence Lebihans,"12, rue des Bouchers",Marseille,13008,France
10,Bottom-Dollar Marketse,Elizabeth Lincoln,23 Tsawassen Blvd.,Tsawassen,T2F 8M4,Canada
11,B's Beverages,Victoria Ashworth,Fauntleroy Circus,London,EC2 5NT,UK
12,Cactus Comidas para llevar,Patricio Simpson,Cerrito 333,Buenos Aires,1010,Argentina
13,Centro comercial Moctezuma,Francisco Chang,Sierras de Granada 9993,México D.F.,05022,Mexico
14,Chop-suey Chinese,Yang Wang,Hauptstr. 29,Bern,3012,Switzerland
15,Comércio Mineiro,Pedro Afonso,"Av. dos Lusíadas, 23",São Paulo,05432-043,Brazil
16,Consolidated Holdings,Elizabeth Brown,Berkeley Gardens 12 Brewery,London,WX1 6LT,UK
17,Drachenblut Delikatessend,Sven Ottlieb,Walserweg 21,Aachen,52066,Germany
18,Du monde entier,Janine Labrune,"67, rue des Cinquante Otages",Nantes,44000,France
19,Eastern Connection,Ann Devon,35 King George,London,WX3 6FW,UK
20,Ernst Handel,Roland Mendel,Kirchgasse 6,Graz,8010,Austria
21,Familia Arquibaldo,Aria Cruz,"Rua Orós, 92",São Paulo,05442-030,Brazil
22,FISSA Fabrica Inter. Salchichas S.A.,Diego Roel,"C/ Moralzarzal, 86",Madrid,28034,Spain
23,Folies gourmandes,Martine Rancé,"184, chaussée de Tournai",Lille,59000,France
24,Folk och fä HB,Maria Larsson,Åkergatan 24,Bräcke,S-844 67,Sweden
25,Frankenversand,Peter Franken,Berliner Platz 43,München,80805,Germany
26,France restauration,Carine Schmitt,"54, rue Royale",Nantes,44000,France
27,Franchi S.p.A.,Paolo Accorti,Via Monte Bianco 34,Torino,10100,Italy
28,Furia Bacalhau e Frutos do Mar,Lino Rodriguez,Jardim das rosas n. 32,Lisboa,1675,Portugal
29,Galería del gastrónomo,Eduardo Saavedra,"Rambla de Cataluña, 23",Barcelona,08022,Spain
30,Godos Cocina Típica,José Pedro Freyre,"C/ Romero, 33",Sevilla,41101,Spain
31,Gourmet Lanchonetes,André Fonseca,"Av. Brasil, 442",Campinas,04876-786,Brazil
32,Great Lakes Food Market,Howard Snyder,2732 Baker Blvd.,Eugene,97403,USA
33,GROSELLA-Restaurante,Manuel Pereira,5ª Ave. Los Palos Grandes,Caracas,1081,Venezuela
34,Hanari Carnes,Mario Pontes,"Rua do Paço, 67",Rio de Janeiro,05454-876,Brazil
35,HILARIÓN-Abastos,Carlos Hernández,"Carrera 22 con Ave. Carlos Soublette #8-35",San Cristóbal,5022,Venezuela
36,Hungry Coyote Import Store,Yoshi Latimer,City Center Plaza 516 Main St.,Elgin,97827,USA
37,Hungry Owl All-Night Grocers,Patricia McKenna,8 Johnstown Road,Cork,,Ireland
38,Island Trading,Helen Bennett,Garden House Crowther Way,Cowes,PO31 7PJ,UK
39,Königlich Essen,Philip Cramer,Maubelstr. 90,Brandenburg,14776,Germany
40,La corne d'abondance,Daniel Tonini,"67, avenue de l'Europe",Versailles,78000,France
41,La maison d'Asie,Annette Roulet,1 rue Alsace-Lorraine,Toulouse,31000,France
42,Laughing Bacchus Wine Cellars,Yoshi Tannamuri,1900 Oak St.,Vancouver,V3F 2K1,Canada
43,Lazy K Kountry Store,John Steel,12 Orchestra Terrace,Walla Walla,99362,USA
44,Lehmanns Marktstand,Renate Messner,Magazinweg 7,Frankfurt a.M.,60528,Germany
45,Let's Stop N Shop,Jaime Yorres,87 Polk St. Suite 5,San Francisco,94117,USA
46,LILA-Supermercado,Carlos González,"Carrera 52 con Ave. Bolívar #65-98 Llano Largo",Barquisimeto,3508,Venezuela
47,LINO-Delicateses,Felipe Izquierdo,Ave. 5 de Mayo Porlamar,I. de Margarita,4980,Venezuela
48,Lonesome Pine Restaurant,Fran Wilson,89 Chiaroscuro Rd.,Portland,97219,USA
49,Magazzini Alimentari Riuniti,Giovanni Rovelli,Via Ludovico il Moro 22,Bergamo,24100,Italy
50,Maison Dewey,Catherine Dewey,Rue Joseph-Bens 532,Bruxelles,B-1180,Belgium
```

---

# 2. Create Customers Table

## Question

Create a `Customers` table to store the CSV data.

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

# 3. Python Program — Read CSV

## Question

Read the customer records from `customers.csv`.

We use Python's built-in `csv` module.

```python
import csv


def read_csv():

    customers = []

    with open("customers.csv", "r", encoding="utf-8") as file:

        reader = csv.reader(file)

        next(reader)   # Skip header

        for row in reader:

            customers.append(row)

    return customers
```

The returned data will look like:

```python
[
    ['1', 'Alfreds Futterkiste', 'Maria Anders',
     'Obere Str. 57', 'Berlin', '12209', 'Germany'],

    ['2', 'Ana Trujillo Emparedados y helados', 'Ana Trujillo',
     'Avda. de la Constitución 2222', 'México D.F.', '05021', 'Mexico'],

    ...
]
```

---

# 4. Python Program — Read CSV and Insert Multiple Records

## Question

Read all customer records from the CSV file and insert them into MySQL using `executemany()`.

```python
import csv

from database import get_connection


def read_csv():

    customers = []

    with open("customers.csv", "r", encoding="utf-8") as file:

        reader = csv.reader(file)

        next(reader)   # Skip header

        for row in reader:

            customers.append(row)

    return customers


def insert_multiple_customers():

    customers = read_csv()

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        INSERT INTO Customers
        (
            CustomerID,
            CustomerName,
            ContactName,
            Address,
            City,
            PostalCode,
            Country
        )
        VALUES (%s, %s, %s, %s, %s, %s, %s)
    """

    cursor.executemany(sql, customers)

    connection.commit()

    print(len(customers), "customers inserted successfully.")

    cursor.close()
    connection.close()


def main():

    insert_multiple_customers()


if __name__ == "__main__":
    main()
```

---

# 5. Program Flow

The important concept in this program is:

```text
customers.csv
      │
      ▼
   csv.reader()
      │
      ▼
   Python List
      │
      ▼
   customers
      │
      ▼
 cursor.executemany()
      │
      ▼
 MySQL Customers Table
```

---

# 6. Understanding `executemany()`

Instead of inserting one record at a time:

```python
cursor.execute(sql, customer1)
cursor.execute(sql, customer2)
cursor.execute(sql, customer3)
```

we can insert all records together:

```python
cursor.executemany(sql, customers)
```

This is the main purpose of this demo.

---

# 7. Important Data Conversion

CSV data is read as **strings**.

For example:

```python
['1', 'Alfreds Futterkiste', 'Maria Anders',
 'Obere Str. 57', 'Berlin', '12209', 'Germany']
```

Even:

```text
1
```

is initially read as a string:

```python
'1'
```

MySQL connector can handle the conversion for the `INT` column in this case.

If we want explicit conversion, we can do:

```python
for row in reader:

    row[0] = int(row[0])

    customers.append(row)
```

---

# 8. Better Version — Using `csv.DictReader`

For teaching purposes, `DictReader` is also useful because it connects CSV column names directly to the database fields.

```python
import csv

from database import get_connection


def read_csv():

    customers = []

    with open("customers.csv", "r", encoding="utf-8") as file:

        reader = csv.DictReader(file)

        for row in reader:

            customers.append((
                int(row["CustomerID"]),
                row["CustomerName"],
                row["ContactName"],
                row["Address"],
                row["City"],
                row["PostalCode"],
                row["Country"]
            ))

    return customers


def insert_multiple_customers():

    customers = read_csv()

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        INSERT INTO Customers
        (
            CustomerID,
            CustomerName,
            ContactName,
            Address,
            City,
            PostalCode,
            Country
        )
        VALUES (%s, %s, %s, %s, %s, %s, %s)
    """

    cursor.executemany(sql, customers)

    connection.commit()

    print(len(customers), "customers inserted successfully.")

    cursor.close()
    connection.close()


def main():

    insert_multiple_customers()


if __name__ == "__main__":
    main()
```

---

# 9. Verify the Data

After running the Python program:

```sql
SELECT *
FROM Customers;
```

Expected:

```text
50 customer records
```

We can also check the count:

```sql
SELECT COUNT(*)
FROM Customers;
```

Expected result:

```text
50
```

---

# 10. Now Use the Same Data for SQL Practice

Once the CSV data has been loaded, we can use the same `Customers` table for the following exercises.

### Question 1

Display all customers.

```sql
SELECT *
FROM Customers;
```

### Question 2

Display customers from Mexico.

```sql
SELECT *
FROM Customers
WHERE Country = 'Mexico';
```

### Question 3

Display customers from Germany.

```sql
SELECT *
FROM Customers
WHERE Country = 'Germany';
```

### Question 4

Display customers from London.

```sql
SELECT *
FROM Customers
WHERE City = 'London';
```

### Question 5

Display customers from Berlin OR London.

```sql
SELECT *
FROM Customers
WHERE City = 'Berlin'
   OR City = 'London';
```

### Question 6

Display customers who are NOT from Germany.

```sql
SELECT *
FROM Customers
WHERE NOT Country = 'Germany';
```

### Question 7

Sort customers by name.

```sql
SELECT *
FROM Customers
ORDER BY CustomerName;
```

### Question 8

Display the first 10 customers.

```sql
SELECT *
FROM Customers
LIMIT 10;
```

### Question 9

Display the first 10 customers alphabetically.

```sql
SELECT *
FROM Customers
ORDER BY CustomerName
LIMIT 10;
```

---

# 11. Final Learning Flow

```text
CSV DATA
   │
   ▼
customers.csv
   │
   ▼
Python csv module
   │
   ▼
Read records
   │
   ▼
Python List
   │
   ▼
executemany()
   │
   ▼
MySQL Customers Table
   │
   ├── SELECT
   ├── WHERE
   ├── OR
   ├── NOT
   ├── ORDER BY
   └── LIMIT
```

## Key Python Concepts

```text
csv.reader()
csv.DictReader()
open()
for loop
list
function
executemany()
commit()
fetchall()
```

## Key MySQL Concepts

```text
CREATE TABLE
INSERT
SELECT
WHERE
OR
NOT
ORDER BY
LIMIT
```

## Main Concept

> **CSV is the input data source. Python reads and prepares the data. `executemany()` sends multiple records to MySQL.**

This same pattern can later be reused for **Products, Employees, Students, Orders, or any other table** by changing the CSV columns and SQL statement.
