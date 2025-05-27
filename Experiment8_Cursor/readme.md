# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

## PROGRAM
```
DECLARE
   -- Simple cursor declaration
   CURSOR emp_cursor IS
      SELECT emp_name, designation FROM employees;

   -- Variables to hold fetched data
   v_emp_name    employees.emp_name%TYPE;
   v_designation employees.designation%TYPE;

   -- Flag to check if data was fetched
   v_found BOOLEAN := FALSE;

BEGIN
   OPEN emp_cursor;

   LOOP
      FETCH emp_cursor INTO v_emp_name, v_designation;
      EXIT WHEN emp_cursor%NOTFOUND;

      v_found := TRUE;  -- At least one record fetched
      DBMS_OUTPUT.PUT_LINE('Name: ' || v_emp_name || ', Designation: ' || v_designation);
   END LOOP;

   CLOSE emp_cursor;

   -- Raise exception if no data was fetched
   IF NOT v_found THEN
      RAISE NO_DATA_FOUND;
   END IF;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employee records found.');
   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```

**Output:**  

![image](https://github.com/user-attachments/assets/1df46f5a-7b0b-4253-b260-4f5295f5bff8)

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

## PROGRAM
```
DECLARE
   -- Input salary range
   v_min_salary NUMBER := 55000;
   v_max_salary NUMBER := 80000;

   -- Parameterized cursor
   CURSOR emp_cursor(p_min NUMBER, p_max NUMBER) IS
      SELECT emp_name, designation, salary
      FROM employees
      WHERE salary BETWEEN p_min AND p_max;

   -- Variables to hold fetched data
   v_name        employees.emp_name%TYPE;
   v_designation employees.designation%TYPE;
   v_salary      employees.salary%TYPE;

   -- Flag to detect if any rows are found
   v_found BOOLEAN := FALSE;

BEGIN
   OPEN emp_cursor(v_min_salary, v_max_salary);

   LOOP
      FETCH emp_cursor INTO v_name, v_designation, v_salary;
      EXIT WHEN emp_cursor%NOTFOUND;

      v_found := TRUE;
      DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Designation: ' || v_designation || ', Salary: ' || v_salary);
   END LOOP;

   CLOSE emp_cursor;

   IF NOT v_found THEN
      RAISE NO_DATA_FOUND;
   END IF;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employees found in the salary range.');

   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END;
```

**Output:**  

![image](https://github.com/user-attachments/assets/87ec1625-4303-4c92-9e70-91479437d731)

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

## PROGRAM
```
DECLARE
   -- Flag to check if any row is found
   v_found BOOLEAN := FALSE;
BEGIN
   -- Cursor FOR loop directly iterates over result set
   FOR emp_rec IN (
      SELECT emp_name, dept_no FROM employees
   ) LOOP
      v_found := TRUE;
      DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name || ', Dept No: ' || emp_rec.dept_no);
   END LOOP;

   -- If no rows were fetched, raise NO_DATA_FOUND manually
   IF NOT v_found THEN
      RAISE NO_DATA_FOUND;
   END IF;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employee records found.');

   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```

**Output:**  

![image](https://github.com/user-attachments/assets/444dfe98-5c17-4076-946f-c0fb4eb611ae)

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

## PROGRAM
```
DECLARE
   -- Cursor to fetch all records
   CURSOR emp_cursor IS
      SELECT * FROM employees;

   -- Record variable using %ROWTYPE
   emp_record employees%ROWTYPE;

   -- Flag to check if data was found
   v_found BOOLEAN := FALSE;

BEGIN
   OPEN emp_cursor;

   LOOP
      FETCH emp_cursor INTO emp_record;
      EXIT WHEN emp_cursor%NOTFOUND;

      v_found := TRUE;

      DBMS_OUTPUT.PUT_LINE(
         'ID: ' || emp_record.emp_id || 
         ', Name: ' || emp_record.emp_name || 
         ', Designation: ' || emp_record.designation || 
         ', Salary: ' || emp_record.salary
      );
   END LOOP;

   CLOSE emp_cursor;

   -- Check if no data was found
   IF NOT v_found THEN
      RAISE NO_DATA_FOUND;
   END IF;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employee records found.');
   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```
**Output:**  

![image](https://github.com/user-attachments/assets/fe27162c-aa73-4ae7-9ae3-fd958e2c7cab)

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

## PROGRAM
```

DECLARE
   -- Target department and increment
   v_dept_no   NUMBER := 10;
   v_increment NUMBER := 1000;
   v_found     BOOLEAN := FALSE;

   -- Cursor to select employees for update
   CURSOR emp_cursor IS
      SELECT emp_id, salary
      FROM employees
      WHERE dept_no = v_dept_no
      FOR UPDATE;

BEGIN
   FOR emp_rec IN emp_cursor LOOP
      v_found := TRUE;

      -- Update salary
      UPDATE employees
      SET salary = emp_rec.salary + v_increment
      WHERE emp_id = emp_rec.emp_id;

      DBMS_OUTPUT.PUT_LINE('Updated salary for Employee ID: ' || emp_rec.emp_id);
   END LOOP;

   IF NOT v_found THEN
      RAISE NO_DATA_FOUND;
   END IF;

   COMMIT;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employees found in department ' || v_dept_no || '.');

   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```

**Output:**  

![image](https://github.com/user-attachments/assets/3144ad25-94d7-4328-a5be-b9cdce6a4a2d)

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

