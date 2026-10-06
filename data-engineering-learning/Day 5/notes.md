Day 5 — CTE, CASE and NULL Handling
Topics Covered
- CTE
- CASE
- IS NULL
- IS NOT NULL
- COALESCE()
CTE
CTE means Common Table Expression.
Basic structure:
WITH cte_name AS (
    SELECT ...
    FROM ...
    WHERE ...
)
SELECT *
FROM cte_name;

Example:
WITH salary_seq1 AS (
    SELECT name, salary, department
    FROM employees
    WHERE salary > 80000
)
SELECT *
FROM salary_seq1
WHERE department = 'IT';

Why use CTE?
A CTE is useful for:
- readability
- breaking complex SQL into steps
- creating an intermediate result
- combining transformations
- making SQL easier to maintain
A CTE is not required simply because the result contains multiple rows.
CASE
CASE allows conditional logic in SQL.
Example:
CASE
    WHEN salary >= 85000 THEN 'High'
    ELSE 'Low'
END AS salary_category

Multiple conditions:
CASE
    WHEN salary >= 85000 THEN 'High'
    WHEN salary >= 70000 THEN 'Medium'
    ELSE 'Low'
END AS salary_category

Important:
CASE
WHEN condition THEN result
ELSE result
END

NULL Handling
Check for NULL:
WHERE salary IS NULL;

Check for non-NULL:
WHERE salary IS NOT NULL;

Do not use:
salary = NULL

Use:
salary IS NULL

COALESCE
COALESCE() returns the first non-NULL value.
Example:
COALESCE(city, 'Unknown') AS city_display

If:
city = Chennai

result:
Chennai

If:
city = NULL

result:
Unknown

Day 6 — SQL Window Functions
Topics Covered
- Window functions
- OVER()
- PARTITION BY
- ORDER BY inside OVER()
- AVG() OVER()
- MAX() OVER()
- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- LAG()
- LEAD()
- FIRST_VALUE()
- LAST_VALUE()
- Combining CTE + Window Functions
GROUP BY vs Window Functions
Important difference:
GROUP BY
→ combines/collapses rows

Window Function
→ keeps individual rows
→ adds a calculation to each row

Example:
AVG(salary) OVER (
    PARTITION BY department
)

This calculates the department average while keeping every employee row.
PARTITION BY
Think:
PARTITION BY → Which group?
ORDER BY     → What sequence?

Example:
LAG(salary) OVER (
    PARTITION BY department
    ORDER BY salary DESC
)

This finds the previous salary within each department.
PARTITION BY is optional.
Without it:
LAG(salary) OVER (
    ORDER BY salary DESC
)

the entire employee dataset is treated as one window.
ROW_NUMBER
Gives every row a unique sequential number.
ROW_NUMBER() OVER (
    PARTITION BY department
    ORDER BY salary DESC
)

Example:
Priya   90000 → 1
John    85000 → 2
Ravi    80000 → 3

RANK
Ties receive the same rank, and the next rank is skipped.
Example:
90000 → 1
85000 → 2
85000 → 2
75000 → 4

DENSE_RANK
Ties receive the same rank, but there are no gaps.
90000 → 1
85000 → 2
85000 → 2
75000 → 3

Memory shortcut
ROW_NUMBER  → unique numbers
RANK        → ties + gaps
DENSE_RANK  → ties + no gaps

LAG
LAG() looks at the previous row.
LAG(salary) OVER (
    ORDER BY salary DESC
)

Example:
Priya   90000 → NULL
John    85000 → 90000
Ravi    80000 → 85000

LEAD
LEAD() looks at the next row.
LEAD(salary) OVER (
    ORDER BY salary DESC
)

Example:
Priya   90000 → 85000
John    85000 → 80000
Ravi    80000 → 75000
Kumar   60000 → NULL

Memory shortcut:
LAG  → previous ←
LEAD → next →

FIRST_VALUE
Returns the first value in the window.
FIRST_VALUE(salary) OVER (
    ORDER BY salary DESC
)

With:
PARTITION BY department

it can be used to find the highest salary within each department.
LAST_VALUE
LAST_VALUE() requires attention to the window frame.
With an ordered window, the default frame can end at the current row, meaning LAST_VALUE() may return the current row's value rather than the last value of the entire partition.
To explicitly get the last value of the complete partition:
LAST_VALUE(salary) OVER (
    PARTITION BY department
    ORDER BY salary DESC
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND UNBOUNDED FOLLOWING
)

Important learning:
LAST_VALUE() is sensitive to the window frame.
