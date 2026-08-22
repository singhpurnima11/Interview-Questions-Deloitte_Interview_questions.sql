# Interview-Questions-Deloitte_Interview_questions.sql
This repository contains solutions to various advanced SQL interview questions, primarily focused on demonstrating proficiency with SQL Server. The goal is to provide clear, efficient, and well-documented SQL queries that can help anyone prepare for technical interviews.

PROBLEM STATEMENT- 
The requirement is to find employees whose salary is higher than the average salary of employees in their respective location. 

TASK -
1. Group employees by location

For example:

Delhi → Employees A, B, C
Mumbai → Employees D, E, F

2. Calculate the average salary for each location

For example:

Delhi → Average = ₹60,000
Mumbai → Average = ₹50,000

3. Compare each employee's salary with their location average

APPROACH -
Step-by-step approach

Step 1 — Identify the grouping factor
The question says “respective location”, so Location is the grouping column.

Step 2 — Calculate location-wise average salary
This gives each employee the average salary for their location.

Step 3 — Compare salaries
Keep only employees whose salary is above their location's average.

Step 4 — Return required columns
SELECT EmpID, Emp_name, Salary, Location
FROM (
    SELECT EmpID,
           Emp_name,
           Salary,
           Location,
           AVG(Salary) OVER (PARTITION BY Location) AS Avg_Salary
    FROM Employee
) e
WHERE Salary > Avg_Salary;

RESULT -
The query returns Mike and James because Mike's salary of ₹70,000 is greater than the Delhi average of ₹60,000, while James's salary of ₹60,000 is greater than the Mumbai average of ₹50,000. Employees whose salaries are equal to or below their location's average are excluded.

---------------------------------------------------------------------------------------------------------------------------------------------------


