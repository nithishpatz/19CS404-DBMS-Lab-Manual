# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Department with the following constraints:
- DepartmentID as INTEGER should be the primary key.
- DepartmentName as TEXT should be unique and not NULL.
- Location as TEXT.

```sql
SQL CODE
CREATE TABLE Department(
DepartmentID INTEGER PRIMARY KEY,
DepartmentName TEXT UNIQUE NOT NULL,
Location TEXT
);
```

**Output:**

![image](https://github.com/user-attachments/assets/131868f0-66a8-4b8e-99a6-4028b8f11e9d)

**Question 2**
---
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.
```
ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021
```

```sql
SQL CODE
INSERT INTO Books (ISBN,Title,Author)
VALUES('978-1234567890','Introduction to AI','John Doe'); 
INSERT INTO Books (ISBN,Title,Author,Publisher,Year)
VALUES('978-9876543210','Deep Learning','Jane Doe','TechPress','2022');
INSERT INTO Books (ISBN,Title,Author,Year) 
VALUES('978-1122334455','Cybersecurity Essentials','Alice Smith','2021');
```

**Output:**

![image](https://github.com/user-attachments/assets/e95674a2-8a12-4f6d-bc9b-71a3b30fe466)

**Question 3**
---
Create a new table named item with the following specifications and constraints:
```
1.item_id as TEXT and as primary key.
2.item_desc as TEXT.
3.rate as INTEGER.
4.icom_id as TEXT with a length of 4.
5.icom_id is a foreign key referencing com_id in the company table.
6.The foreign key should cascade updates and deletes.
7.item_desc and rate should not accept NULL.
```

```sql
SQL CODE
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT CHECK(length(icom_id)=4),
FOREIGN KEY (icom_id) REFERENCES company(com_id)
ON UPDATE CASCADE
ON DELETE CASCADE
);
```

**Output:**

![image](https://github.com/user-attachments/assets/d7d808cd-531c-4bc0-a3e8-9fc7d50e265e)

**Question 4**
---
Write a SQL query to Add a new column State as text in the Student_details table.
Sample table: Student_details
```

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
```

```sql
SQL CODE
ALTER TABLE Student_details
ADD COLUMN State TEXT;
```

**Output:**

![image](https://github.com/user-attachments/assets/1530aa7c-f583-4515-afa8-f45f54d5f3b6)

**Question 5**
---
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

```sql
SQL CODE
INSERT INTO Products(ProductID, Name, Category,Price,Stock)
VALUES(101,'Laptop','Electronics', 1500, 50);

```

**Output:**

![image](https://github.com/user-attachments/assets/386e6a61-da50-4fdf-bff1-f9be2d2fd41b)

**Question 6**
---
Create a table named Locations with the following columns:

- LocationID as INTEGER
- LocationName as TEXT
- Address as TEXT

```sql
SQL CODE
CREATE TABLE Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**

![image](https://github.com/user-attachments/assets/a6b4ffb4-8566-4a28-8abf-56bad07705a4)

**Question 7**
---
Insert all customers from Old_customers into Customers
Table attributes are CustomerID, Name, Address, Email

```sql
SQL CODE
INSERT INTO Customers(CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email 
FROM Old_customers;

```

**Output:**

![image](https://github.com/user-attachments/assets/33bdd1f8-340e-47e8-918d-6f7240d91199)

**Question 8**
---
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.
Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```

```sql
SQL CODE
ALTER TABLE customer
ADD COLUMN discount DECIMAL(5,2);
```

**Output:**

![image](https://github.com/user-attachments/assets/aaa5683b-4d7e-41b5-bc0c-ef1fb1ac328d)

**Question 9**
---
Create a table named ProjectAssignments with the following constraints:
- AssignmentID as INTEGER should be the primary key.
- EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
- ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
- AssignmentDate as DATE should be NOT NULL.

```sql
SQL CODE
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID) 
);
```

**Output:**

![image](https://github.com/user-attachments/assets/994a592f-f7e8-45e8-90ce-a50478105b6a)

**Question 10**
---
Create a new table named contacts with the following specifications:
- contact_id as INTEGER and primary key.
- first_name as TEXT and not NULL.
- last_name as TEXT and not NULL.
- email as TEXT.
- phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
SQL CODE
CREATE TABLE contacts(
contact_id INTEGER PRIMARY KEY,
first_name TEXT NOT NULL,
last_name  NOT NULL,
email TEXT,
phone TEXT NOT NULL CHECK (length(phone) >= 10)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/da798bcc-7895-4df9-9afd-2df8f9736ef0)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
