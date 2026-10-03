# Day 2 – SQL SELECT, WHERE, ORDER BY

## 1. SELECT

SELECT is used to specify the columns we want to retrieve.

Example:

SELECT name, salary
FROM employees;

To retrieve all columns:

SELECT *
FROM employees;

---

## 2. WHERE

WHERE is used to filter rows based on a condition.

Example:

SELECT name, salary
FROM employees
WHERE department = 'IT';

This returns only employees from the IT department.

Common comparison operators:

=       Equal
<>      Not equal
>       Greater than
<       Less than
>=      Greater than or equal
<=      Less than or equal

Example:

SELECT name, salary
FROM employees
WHERE salary > 75000;

---

## 3. AND

AND requires both conditions to be true.

Example:

SELECT name, department, salary
FROM employees
WHERE department = 'IT'
AND salary > 80000;

---

## 4. OR

OR requires at least one condition to be true.

Example:

SELECT name, department, salary
FROM employees
WHERE salary > 80000
OR department = 'IT';

Important:

Ravi has a salary of 80000 but is still included because
his department is IT.

---

## 5. ORDER BY

ORDER BY is used to sort the result.

Ascending:

ORDER BY salary ASC;

Descending:

ORDER BY salary DESC;

DESC means highest to lowest.

Example:

SELECT name, salary
FROM employees
ORDER BY salary DESC;

---

## 6. Combining SELECT + WHERE + ORDER BY

Example:

SELECT name, salary
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC;

Meaning:

SELECT → Which columns?
WHERE → Which rows?
ORDER BY → In what order?

---

## 7. Today's Practice Table

employees

employee_id | name   | department | salary | city
------------|--------|------------|--------|---------
101         | Ravi   | IT         | 80000  | Chennai
102         | Kumar  | HR         | 60000  | Bangalore
103         | Priya  | IT         | 90000  | Chennai
104         | Anitha | Finance    | 75000  | Mumbai
105         | John   | IT         | 85000  | Chennai

---

## 8. Queries I Practiced

### IT employees

SELECT name, salary
FROM employees
WHERE department = 'IT';

### IT employees, highest salary first

SELECT name, salary
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC;

### Salary greater than 75000

SELECT name, salary
FROM employees
WHERE salary > 75000
ORDER BY salary DESC;

### Salary greater than 80000 OR IT department

SELECT name, department, salary
FROM employees
WHERE salary > 80000
OR department = 'IT'
ORDER BY salary DESC;

---

## 9. My Day 2 Understanding

SELECT = What columns do I need?

WHERE = What rows do I need?

ORDER BY = How should I sort the result?

AND = Both conditions must be true.

OR = At least one condition must be true.

DESC = Highest to lowest.

ASC = Lowest to highest.

---

## 10. Day 2 Learning

Today I practiced SQL instead of only reading SQL.

I created a sample employees table, inserted data,
handled a schema mismatch in Databricks, and practiced
SELECT, WHERE, comparison operators, AND, OR and ORDER BY.
