## LeetCode 1661

1661. Average Time of Process per Machine
https://leetcode.com/problems/average-time-of-process-per-machine/description/?envType=study-plan-v2&envId=top-sql-50

## LeetCode 1280
https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50

## if else in sql

1. Simple CASE (Like a switch statement)
This form compares a single column or expression against several specific values.

Syntax:

SQL

CASE column_name
    WHEN value_1 THEN result_1
    WHEN value_2 THEN result_2
    ...
    ELSE else_result
END
Example: Let's say we have a JobApplicants table with a status column containing single letters: 'A' for Approved, 'R' for Rejected, 'P' for Pending. We want to display the full text.

Sample Data:
| applicant_id | status |
|--------------|--------|
| 101 | A |
| 102 | P |
| 103 | R |

Query:

SQL

SELECT
    applicant_id,
    CASE status  -- The column we are checking
        WHEN 'A' THEN 'Approved'
        WHEN 'R' THEN 'Rejected'
        WHEN 'P' THEN 'Pending'
        ELSE 'Unknown Status'
    END AS full_status
FROM
    JobApplicants;
Result:
| applicant_id | full_status |
|--------------|---------------|
| 101 | Approved |
| 102 | Pending |
| 103 | Rejected |

2. Searched CASE (Like an if / else if / else chain)
This is the more powerful and common form. Each WHEN clause contains its own, independent logical condition. This allows you to use operators like >, <, BETWEEN, LIKE, etc.

This is the type you saw in our LeetCode solutions.

Syntax:

SQL

CASE
    WHEN condition_1 THEN result_1
    WHEN condition_2 THEN result_2
    ...
    ELSE else_result
END
Example: Let's categorize employees based on their salary from an Employees table.

Sample Data:
| employee_name | salary |
|---------------|--------|
| Alice | 120000 |
| Bob | 85000 |
| Charlie | 45000 |

Query:

SQL

SELECT
    employee_name,
    salary,
    CASE
        WHEN salary >= 100000 THEN 'Senior Level'
        WHEN salary >= 60000  THEN 'Mid Level'
        ELSE 'Entry Level'
    END AS salary_grade
FROM
    Employees;
Result:
| employee_name | salary | salary_grade |
|---------------|--------|--------------|
| Alice | 120000 | Senior Level |
| Bob | 85000 | Mid Level |
| Charlie | 45000 | Entry Level |

Advanced Use Case: Conditional Aggregation
This is one of the most powerful uses of CASE. You can use it inside an aggregate function like SUM() or COUNT() to perform calculations on only a subset of your data.

Problem: You have a Sales table and you want to see the total sales for 2024 and 2025 in separate columns, all in one query.

Sample Data:
| sale_id | sale_year | amount |
|---------|-----------|--------|
| 1 | 2024 | 100 |
| 2 | 2025 | 150 |
| 3 | 2024 | 50 |
| 4 | 2025 | 200 |

Query:

SQL

SELECT
    -- Sum the amount ONLY IF the year is 2024, otherwise add 0
    SUM(CASE WHEN sale_year = 2024 THEN amount ELSE 0 END) AS sales_2024,
    
    -- Sum the amount ONLY IF the year is 2025, otherwise add 0
    SUM(CASE WHEN sale_year = 2025 THEN amount ELSE 0 END) AS sales_2025
FROM
    Sales;
Result:
| sales_2024 | sales_2025 |
|------------|------------|
| 150 | 350 |

This technique is incredibly useful for creating summary reports and pivoting data from rows into columns.

Important Rules to Remember
END is Mandatory: Every CASE statement must be closed with an END keyword. Forgetting it is a common syntax error.

Order Matters: The WHEN conditions are evaluated in the order they are written. The statement will stop and return the result for the first WHEN condition that evaluates to true.

Wrong Order Example:

SQL

-- This is WRONG because 120000 is also > 60000, so it will stop at the first condition
CASE
    WHEN salary >= 60000  THEN 'Mid Level'  -- This condition is met first
    WHEN salary >= 100000 THEN 'Senior Level'
    ELSE 'Entry Level'
END

## Leetcodd 1934
https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50


## sql syntax
# module operation, not equal and difference between single quotes '' and double quotes ""
1. The MOD Function (Modulo)
Purpose: The MOD function is used to find the remainder of a division operation.

Syntax: MOD(number, divisor)

Common Use Case: Checking for odd or even numbers. This is extremely useful for filtering alternating rows or IDs.

MOD(id, 2) = 1 checks for odd numbers.

MOD(id, 2) = 0 checks for even numbers.

2. The 'Not Equal' Operator
Purpose: Used in a WHERE clause to filter out rows where a column has a specific value.

Standard Syntax: <>

Example: WHERE description <> 'boring'

Alternative Syntax: !=

This works in many systems like MySQL and PostgreSQL, but <> is the most universally accepted ANSI standard. It's safer to use <> for maximum portability.

3. Single Quotes vs. Double Quotes (A Critical Distinction)
Single Quotes ('):

ALWAYS use single quotes for string literals. A string literal is any fixed piece of text.

Examples: 'boring', 'John Doe', '2025-09-05'

Double Quotes ("):

Used for identifiers (like table or column names). You typically only need to use them if your column name has a space, special character, or is a reserved keyword.

Example: SELECT "First Name" FROM Employees;

