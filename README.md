# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### PROGRAM
```

CREATE OR REPLACE PROCEDURE find_square (p_num IN NUMBER) AS
   v_square NUMBER;
BEGIN
   -- Compute the square of the input number
   v_square := p_num * p_num;

   -- Display the result using DBMS_OUTPUT.PUT_LINE
   DBMS_OUTPUT.PUT_LINE('Square of ' || p_num || ' is ' || v_square);
END;
```

**Expected Output:**  

![image](https://github.com/user-attachments/assets/b41cd693-bf85-4778-b477-a30e3739ed23)

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### PROGRAM
```

DECLARE
   v_result NUMBER;
BEGIN
   -- Step 3: Call the function with input 5
   v_result := get_factorial(5);

   -- Step 4: Display the result
   DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || v_result);
END;
```
**Expected Output:**  

![image](https://github.com/user-attachments/assets/b1333ea8-c61e-48bc-99a4-47065a4a3bdd)

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### PROGRAM 
```

CREATE OR REPLACE PROCEDURE check_even_odd (p_num IN NUMBER) AS
BEGIN
   -- Step 2: Use MOD function to check if the number is even or odd
   IF MOD(p_num, 2) = 0 THEN
      DBMS_OUTPUT.PUT_LINE(p_num || ' is Even');
   ELSE
      DBMS_OUTPUT.PUT_LINE(p_num || ' is Odd');
   END IF;
END;
```
**Expected Output:**  

![image](https://github.com/user-attachments/assets/94dc69eb-ba30-426a-93ac-08a377d986ee)

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### PROGRAM
```

DECLARE
   v_result NUMBER;
BEGIN
   -- Call the function with input 1234
   v_result := reverse_number(1234);

   -- Display the result
   DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || v_result);
END;
```

**Expected Output:**  

![image](https://github.com/user-attachments/assets/24aa1c41-1bf6-4985-93c5-9bde56e0a7b9)

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### PROGRAM
```
CREATE OR REPLACE PROCEDURE print_table (p_num IN NUMBER) AS
BEGIN
   -- Step 2: Loop from 1 to 10 to display the multiplication table
   FOR i IN 1..10 LOOP
      DBMS_OUTPUT.PUT_LINE(p_num || ' x ' || i || ' = ' || (p_num * i));
   END LOOP;
END;
```

**Expected Output:**  

![image](https://github.com/user-attachments/assets/9a12c35e-0b9b-48eb-a916-b7fa4b448855)


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
