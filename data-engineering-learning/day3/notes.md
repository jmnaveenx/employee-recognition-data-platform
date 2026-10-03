# Day 3 — SQL JOINs

## Topics Covered

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN
- JOIN conditions
- NULL handling
- JOIN cardinality
- One-to-many relationships
- Finding unmatched records

---

## 1. INNER JOIN

Returns only records that have a matching key in both tables.

```sql
SELECT *
FROM employees AS e
INNER JOIN recognitions AS r
    ON e.employee_id = r.employee_id;

Matching employee IDs:
103, 104, 105
2. LEFT JOIN
Keeps all records from the left table and matching records from the right table.
SELECT *
FROM employees AS e
LEFT JOIN recognitions AS r
    ON e.employee_id = r.employee_id;

Employees without recognitions appear with NULL recognition columns.
3. RIGHT JOIN
Keeps all records from the right table and matching records from the left table.
SELECT *
FROM employees AS e
RIGHT JOIN recognitions AS r
    ON e.employee_id = r.employee_id;

Recognitions without matching employees appear with NULL employee columns.
4. FULL OUTER JOIN
Keeps all records from both tables.
SELECT *
FROM employees AS e
FULL OUTER JOIN recognitions AS r
    ON e.employee_id = r.employee_id;

This showed:
- Employees without recognitions
- Employees with recognitions
- Recognitions without employees
5. JOIN Cardinality
One employee can have multiple recognition records.
Example:
Employee 103 — Priya
    |
    +-- Recognition 1 → 3000 points
    +-- Recognition 6 → 2500 points

One employee → many recognition records.
The JOIN therefore produces two rows for Priya.
Important concept:
JOIN cardinality can cause rows to multiply.

Before calculating aggregates, always understand the grain of each table.
6. Finding Orphan Records
To find recognition records that don't have a matching employee:
SELECT ...
FROM recognitions r
LEFT JOIN employees e
    ON e.employee_id = r.employee_id
WHERE e.employee_id IS NULL;

This identifies recognition records for employees that don't exist in the employee master table.
7. Finding Employees Without Recognition
Using a RIGHT JOIN:
SELECT ...
FROM recognitions r
RIGHT JOIN employees e
    ON e.employee_id = r.employee_id
WHERE r.recognition_id IS NULL;

This identifies employees who don't have a recognition record.
Key Mental Model
INNER JOIN → matching records only

LEFT JOIN → everything from LEFT table

RIGHT JOIN → everything from RIGHT table

FULL OUTER JOIN → everything from BOTH tables

Data Engineering Takeaway
JOINs are not only about combining tables.
They are also useful for:
- Data-quality checks
- Finding missing reference data
- Identifying orphan records
- Understanding table relationships
- Detecting unexpected row multiplication
- Preparing data for aggregation
