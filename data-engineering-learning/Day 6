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

Practical Day 6 Exercise
We combined:
CTE
+
LAG()
+
PARTITION BY
+
salary calculation
+
CASE

The transformation calculated:
salary - previous_salary

and classified the result.
Example:
John
85000 - 90000 = -5000
→ Salary Decreased

Ravi
80000 - 85000 = -5000
→ Salary Decreased

First employee in each department:
previous_salary = NULL
→ No Previous

Day 6 Interview Pattern — Top N per Group
We solved:
Find the top 2 employees in each department.

Final query:
WITH rank AS (
    SELECT
        name,
        department,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS ROWN
    FROM employees
)
SELECT *
FROM rank
WHERE ROWN <= 2;

Pattern to remember
PARTITION BY department
        ↓
ORDER BY salary DESC
        ↓
ROW_NUMBER()
        ↓
CTE
        ↓
WHERE rank <= N

This is an important SQL/Data Engineering interview pattern.
Day 4–6 Status
Day 4 → SQL Aggregations       ✅
Day 5 → CTE / CASE / NULL      ✅
Day 6 → Window Functions       ✅

Git status:
Day 1 → committed ✅
Day 2 → committed ✅
Day 3 → committed ✅
Day 4 → pending
Day 5 → pending
Day 6 → pending
