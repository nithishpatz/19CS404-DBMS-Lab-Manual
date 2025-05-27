# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Increase the selling price per unit by 5% for product ID 15 who's sale is on '2023-01-31'.
sales(sale_id,sale_date,product_id,quantity,sell_price,total_sell_price)

```sql
UPDATE sales 
SET sell_price = sell_price * 1.05
WHERE product_id = 15 
AND sale_date = '2023-01-31';
```

**Output:**

![image](https://github.com/user-attachments/assets/88542a2f-63ea-4ed6-b96d-bbff89046950)

**Question 2**
---
Write a SQL statement to double the availability of the product with product_id 1.
```
products table

---------------
product_id
product_name
category_id
availability
```

```sql
UPDATE products
SET availability = 2 * availability 
WHERE product_id = 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/31e17395-bc88-43b9-8325-9b4de8d45cd5)

**Question 3**
---
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.
```
Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id
```

```sql
UPDATE Products
SET reorder_lvl = 20
WHERE quantity < 10
AND category = 'Snacks';
```

**Output:**

![image](https://github.com/user-attachments/assets/3a468be6-8cc4-49be-b97d-8f0d43bd9c29)

**Question 4**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.
```
products table

---------------
product_id
product_name
category_id
availability
```

```sql
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_id = 4;
```

**Output:**

![image](https://github.com/user-attachments/assets/698ae9f9-c6ee-4ae7-989a-5cecec2b1c17)

**Question 5**
---
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.
Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.
```
Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
```

```sql
UPDATE Employees
SET salary =
CASE 
WHEN department_id = 40 THEN ROUND(salary * 1.25 ,2)
WHEN department_id = 90 THEN ROUND(salary * 1.15 ,2)
WHEN department_id = 110 THEN ROUND(salary * 1.10 ,2)
ELSE salary
END;
```

**Output:**

![image](https://github.com/user-attachments/assets/a9b8d350-3301-483a-b5d9-902c0440f6b0)

**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'WORKING_AREA' is 'New York'.
Sample table: Customer
```
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```

```sql
DELETE FROM Customer
WHERE WORKING_AREA = 'New York';
```

**Output:**

![image](https://github.com/user-attachments/assets/783c4572-91d3-413e-a607-b667a53e456c)

**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' contains the substring 'Holmes'.
Sample table: Customer
```
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```

```sql
DELETE FROM Customer
WHERE CUST_NAME LIKE '%Holmes%';
```

**Output:**

![image](https://github.com/user-attachments/assets/5c6cc0a6-ba4d-4d87-8220-96e1f5494358)

**Question 8**
---
Write a SQL query to Delete All Doctors with a NULL Last Name.
- Sample table: Doctors
- attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE last_name IS NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/d679c15a-f249-49da-9400-cf84fc44206d)

**Question 9**
---
Write a SQL query to Delete all Doctors whose Specialization is either 'Pediatrics' or 'Cardiology' and Last Name is Brown.
- Sample table: Doctors
- attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE specialization IN ('Pediatrics','Cardiology')
AND last_name = 'Brown';
```

**Output:**

![image](https://github.com/user-attachments/assets/1e39da2b-7c39-4ec5-81a5-16ca8ae1dc61)

**Question 10**
---
Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000
Sample table: Customer
```
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```

```sql
DELETE FROM Customer
WHERE CUST_NAME LIKE 'M%'
AND PAYMENT_AMT < 3000;
```

**Output:**

![image](https://github.com/user-attachments/assets/44ecc6fe-d922-4951-b39a-205a7078663a)

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
