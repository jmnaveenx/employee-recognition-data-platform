Day 4 — SQL Aggregations
Topics Covered
- GROUP BY
- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()
- HAVING
- ORDER BY with aggregate results
- Difference between WHERE and HAVING
Key Concepts
GROUP BY
GROUP BY creates groups of rows based on a column.
Example:
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department;

Result:
IT       255000
Finance   75000
HR        60000

Aggregate Functions
COUNT() → number of rows
SUM()   → total
AVG()   → average
MIN()   → minimum
MAX()   → maximum

HAVING vs WHERE
WHERE
→ filters individual rows
→ happens before GROUP BY

GROUP BY
→ creates groups

HAVING
→ filters groups
→ happens after GROUP BY

Example:
SELECT department, COUNT(employee_id)
FROM employees
GROUP BY department
HAVING COUNT(employee_id) > 1;

Result:
IT    3

Important Learning
ORDER BY is used for sorting the final result.
For example:
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 75000
ORDER BY avg_salary DESC;
