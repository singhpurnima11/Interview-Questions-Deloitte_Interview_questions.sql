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

SQL Query to find the employees whose salary is greater than the average salary of employees in their respective location
We suppose there is a table for Employee table named - EMPLOYEE 
Attribute - Emp_ID, Emp_Name,Salary,Location
/*create Table Employees (
EmpID int, 
Emp_name varchar(30), 
Manager_id int, 
Salary int, 
Location varchar(30)
)
INSERT INTO Employees (EmpID, Emp_name, Manager_id, Salary, Location)
VALUES
(1, 'John Smith', NULL, 120000, 'New York'),
(2, 'Alice Johnson', 1, 100000, 'Los Angeles'),
(3, 'Robert Brown', 1, 105000, 'Chicago'),
(4, 'Emma Davis', 2, 95000, 'Miami'),
(5, 'Michael Miller', 2, 90000, 'Boston'),
(6, 'Sophia Wilson', 3, 88000, 'Dallas'),
(7, 'Daniel Garcia', 3, 86000, 'Seattle'),
(8, 'Olivia Martinez', 4, 83000, 'Houston'),
(9, 'James Anderson', 5, 81000, 'Atlanta'),
(10, 'Isabella Lee', 5, 80000, 'San Francisco'),
(11, 'Henry Thomas', 6, 78000, 'Austin'),
(12, 'Emily Walker', 6, 76000, 'Philadelphia'),
(13, 'Alexander Scott', 7, 74000, 'Denver'),
(14, 'Grace Turner', 7, 72000, 'Phoenix'),
(15, 'Benjamin Hill', 8, 70000, 'San Diego'),
(16, 'Amelia Carter', 8, 69000, 'Dallas'),
(17, 'Ethan Lewis', 9, 68000, 'Chicago'),
(18, 'Charlotte Nelson', 9, 67000, 'Houston'),
(19, 'Mason Young', 10, 66000, 'Miami'),
(20, 'Abigail Perez', 10, 65000, 'Seattle'),
(21, 'Liam Clark', 1, 100000, 'New York'),
(22, 'Ava Hernandez', 1, 99000, 'Los Angeles'),
(23, 'Noah King', 2, 98000, 'San Francisco'),
(24, 'Mia Hall', 2, 97000, 'Boston'),
(25, 'Lucas Allen', 3, 96000, 'Dallas'),
(26, 'Harper Wright', 3, 94000, 'Philadelphia'),
(27, 'Elijah Baker', 4, 93000, 'Atlanta'),
(28, 'Evelyn Gonzalez', 4, 92000, 'Houston'),
(29, 'William Adams', 5, 91000, 'Denver'),
(30, 'Sophia Rodriguez', 5, 90000, 'Phoenix'),
(31, 'James Foster', 6, 88000, 'San Diego'),
(32, 'Amelia Howard', 6, 86000, 'Chicago'),
(33, 'Alexander Bell', 7, 85000, 'Miami'),
(34, 'Luna Russell', 7, 84000, 'Seattle'),
(35, 'Oliver Stewart', 8, 83000, 'Los Angeles'),
(36, 'Aria Morris', 8, 82000, 'Boston'),
(37, 'Jack Hughes', 9, 81000, 'New York'),
(38, 'Scarlett Simmons', 9, 80000, 'Dallas'),
(39, 'Henry Jenkins', 10, 79000, 'San Francisco'),
(40, 'Ella Coleman', 10, 78000, 'Philadelphia'),
(41, 'Jacob Cook', 1, 115000, 'Chicago'),
(42, 'Avery Powell', 1, 110000, 'Miami'),
(43, 'Lucas Ward', 2, 108000, 'Atlanta'),
(44, 'Isabella Butler', 2, 107000, 'Dallas'),
(45, 'Michael Barnes', 3, 106000, 'Phoenix'),
(46, 'Mia Mitchell', 3, 104000, 'Houston'),
(47, 'Daniel Brooks', 4, 103000, 'Denver'),
(48, 'Charlotte Sanders', 4, 102000, 'Seattle'),
(49, 'Ethan Murphy', 5, 101000, 'San Diego'),
(50, 'Emily Reed', 5, 100000, 'Boston');
*/

Select Emp_Name,Emp_ID,Salary,Location
FROM
(Select Emp_Name,Emp_ID,Salary,Location,AVG(Salary) OVER (PARTITION BY Location) AS AVG_Salary)
WHERE Salary>AVG_Salary
