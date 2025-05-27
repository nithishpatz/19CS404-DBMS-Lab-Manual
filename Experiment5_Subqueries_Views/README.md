# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
-- 
![Screenshot 2025-04-30 114151](https://github.com/user-attachments/assets/db98b05a-4f0f-4e6d-8d1b-f3c173eab25d)

```sql
--
select medication_id,medication_name,dosage from Medications
where dosage=(
     select min(dosage) from Medications);
```

**Output:**

![Screenshot 2025-04-30 114159](https://github.com/user-attachments/assets/65d0b034-1704-4420-a79f-99d910ea8381)


**Question 2**
---
-- 
![Screenshot 2025-04-30 114207](https://github.com/user-attachments/assets/e2fb59f3-85b9-45d2-8bdb-658896b3012c)

```sql
--
select * from CUSTOMERS
where SALARY>4500;
```

**Output:**

![Screenshot 2025-04-30 114215](https://github.com/user-attachments/assets/6fd561b9-6127-42e3-8feb-18248af4d963)


**Question 3**
---
-- 
![Screenshot 2025-04-30 114253](https://github.com/user-attachments/assets/bee8c28b-b780-4971-8c08-9db3a1840943)

```sql
--
SELECT orders.ord_no,orders.purch_amt, orders.ord_date, orders.customer_id, orders.salesman_id
FROM orders 
JOIN 
    salesman ON orders.salesman_id = salesman.salesman_id
WHERE 
    salesman.city = 'New York';

```

**Output:**

![Screenshot 2025-04-30 114301](https://github.com/user-attachments/assets/75ca9067-8513-41e8-b418-0694d92f0cbc)


**Question 4**
---
--
![Screenshot 2025-04-30 114311](https://github.com/user-attachments/assets/d032402e-04f7-4bcc-89dc-91c515f9260c)

```sql
--
SELECT grade, COUNT(*)
FROM customer
GROUP BY grade
HAVING grade > (
    SELECT AVG(grade)
    FROM customer
    WHERE city = 'New York'
);
```

**Output:**

![Screenshot 2025-04-30 114316](https://github.com/user-attachments/assets/f220aaa2-a012-421d-8bd1-bf11245a83e3)


**Question 5**
---
-- 
![Screenshot 2025-04-30 114329](https://github.com/user-attachments/assets/b4dcf211-9c18-4311-8b78-7887128831e4)

```sql
--
select id,name,age,city,income from Employee 
where age<(
      select avg(age) from Employee
      where income>1000000);
```

**Output:**

![Screenshot 2025-04-30 114338](https://github.com/user-attachments/assets/867572a6-e3f5-4125-ab4e-2afa8181c517)


**Question 6**
---
--
![Screenshot 2025-04-30 114346](https://github.com/user-attachments/assets/2a51254c-10f7-4d8d-a1de-905801f58990)

```sql
--
select * from CUSTOMERS
where SALARY=1500;
```

**Output:**

![Screenshot 2025-04-30 114353](https://github.com/user-attachments/assets/4369e5ef-657f-423f-b7d7-3356889bf916)


**Question 7**
---
-- 
![Screenshot 2025-04-30 114400](https://github.com/user-attachments/assets/8f0bcc69-bc63-4d74-827f-86ba868957a7)

```sql
--
SELECT student_id, student_name, subject, grade
FROM Grades
WHERE grade = (
    SELECT MIN(grade)
    FROM Grades AS g
    WHERE g.subject = Grades.subject
);
```

**Output:**

![Screenshot 2025-04-30 114409](https://github.com/user-attachments/assets/49f551a6-c463-48ac-84d3-18a73c4c37cc)

**Question 8**
---
-- 
![Screenshot 2025-04-30 114418](https://github.com/user-attachments/assets/0d769c70-416d-4057-b094-9b799511a794)

```sql
--
select ord_no,purch_amt,ord_date,customer_id,salesman_id from ORDERS
where purch_amt>(
      select avg(purch_amt ) from ORDERS
      where ord_date ='2012-10-10');
```

**Output:**

![Screenshot 2025-04-30 114427](https://github.com/user-attachments/assets/f438ab12-3573-4644-98f1-ec09f6d592e7)


**Question 9**
---
--
![Screenshot 2025-04-30 114434](https://github.com/user-attachments/assets/97d951c0-a9f4-4095-9b2c-4d8f141a1fab)

```sql
--
select *from CUSTOMERS
where id in(
      select ID from customers
      where address='Delhi' and age<30);
```

**Output:**

![Screenshot 2025-04-30 114442](https://github.com/user-attachments/assets/9883fdf4-bec4-4211-b292-8154b600edfb)


**Question 10**
---
-- 
![Screenshot 2025-04-30 114450](https://github.com/user-attachments/assets/07443b7a-f239-4af0-9432-fb38a8fc1209)

```sql
--
select commission from salesman
where salesman_id in(
       select salesman_id from customer
       where city='Paris');
```

**Output:**

![Screenshot 2025-04-30 114455](https://github.com/user-attachments/assets/6b2b1f9a-cd78-404b-8750-f4bed5471537)



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
