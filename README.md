# procore_sql_interview_questions

/*
CoderPad provides a basic SQL sandbox with the following schema.
You can also use commands like `show tables` and `desc employees`

Preamble: 

The below ERD provides a detailed view of the data structures for the questions. Feel free to ask questions about the tables, columns, and data or completed data exploration.

employees                             projects
+---------------+---------+           +---------------+---------+
| id            | int     |<----+  +->| id            | int     |
| first_name    | varchar |     |  |  | title         | varchar |
| last_name     | varchar |     |  |  | start_date    | date    |
| salary        | int     |     |  |  | end_date      | date    |
| department_id | int     |--+  |  |  | budget        | int     |
+---------------+---------+  |  |  |  +---------------+---------+
                             |  |  |
departments                  |  |  |  employees_projects
+---------------+---------+  |  |  |  +---------------+---------+
| id            | int     |<-+  |  +--| project_id    | int     |
| name          | varchar |     +-----| employee_id   | int     |
+---------------+---------+           +---------------+---------+
*/

/*SELECT e.first_name, e.last_name, e.salary,
  d.name as department_name
FROM employees   AS e
JOIN departments AS d ON e.department_id = d.id;
*/

==========================================
Create Table Statement
==========================================

-- Create the departments table
CREATE TABLE departments (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

-- Create the employees table
CREATE TABLE employees (
    id INT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    salary INT,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(id)
);

-- Create the projects table
CREATE TABLE projects (
    id INT PRIMARY KEY,
    title VARCHAR(100),
    start_date DATE,
    end_date DATE,
    budget INT
);

-- Create the employees_projects table (junction table for many-to-many relationship)
CREATE TABLE employees_projects (
    id INT PRIMARY KEY,
    project_id INT,
    employee_id INT,
    FOREIGN KEY (project_id) REFERENCES projects(id),
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);


-- Insert data into the departments table
INSERT INTO departments (id, name) VALUES
(1, 'Department_1'),
(2, 'Department_2'),
(3, 'Department_3'),
(4, 'Department_4'),
(5, 'Department_5');

-- Insert data into the employees table
INSERT INTO employees (id, first_name, last_name, salary, department_id) VALUES
(1, 'FirstName_1', 'LastName_1', 75000, 1),
(2, 'FirstName_2', 'LastName_2', 85000, 2),
(3, 'FirstName_3', 'LastName_3', 62000, 3),
(4, 'FirstName_4', 'LastName_4', 94000, 4),
(5, 'FirstName_5', 'LastName_5', 53000, 5),
(6, 'FirstName_6', 'LastName_6', 68000, 1),
(7, 'FirstName_7', 'LastName_7', 102000, 2),
(8, 'FirstName_8', 'LastName_8', 59000, 3),
(9, 'FirstName_9', 'LastName_9', 87000, 4),
(10, 'FirstName_10', 'LastName_10', 72000, 5),
(11, 'FirstName_11', 'LastName_11', 48000, 1),
(12, 'FirstName_12', 'LastName_12', 95000, 2),
(13, 'FirstName_13', 'LastName_13', 70000, 3),
(14, 'FirstName_14', 'LastName_14', 86000, 4),
(15, 'FirstName_15', 'LastName_15', 51000, 5),
(16, 'FirstName_16', 'LastName_16', 63000, 1),
(17, 'FirstName_17', 'LastName_17', 110000, 2),
(18, 'FirstName_18', 'LastName_18', 55000, 3),
(19, 'FirstName_19', 'LastName_19', 79000, 4),
(20, 'FirstName_20', 'LastName_20', 72000, 5),
(21, 'FirstName_21', 'LastName_21', 67000, 1),
(22, 'FirstName_22', 'LastName_22', 89000, 2),
(23, 'FirstName_23', 'LastName_23', 93000, 3),
(24, 'FirstName_24', 'LastName_24', 61000, 4),
(25, 'FirstName_25', 'LastName_25', 72000, 5),
(26, 'FirstName_26', 'LastName_26', 84000, 1),
(27, 'FirstName_27', 'LastName_27', 58000, 2),
(28, 'FirstName_28', 'LastName_28', 102000, 3),
(29, 'FirstName_29', 'LastName_29', 69000, 4),
(30, 'FirstName_30', 'LastName_30', 50000, 5),
(31, 'FirstName_31', 'LastName_31', 88000, 1),
(32, 'FirstName_32', 'LastName_32', 78000, 2),
(33, 'FirstName_33', 'LastName_33', 71000, 3),
(34, 'FirstName_34', 'LastName_34', 93000, 4),
(35, 'FirstName_35', 'LastName_35', 57000, 5),
(36, 'FirstName_36', 'LastName_36', 60000, 1),
(37, 'FirstName_37', 'LastName_37', 98000, 2),
(38, 'FirstName_38', 'LastName_38', 82000, 3),
(39, 'FirstName_39', 'LastName_39', 87000, 4),
(40, 'FirstName_40', 'LastName_40', 72000, 5),
(41, 'FirstName_41', 'LastName_41', 75000, 1),
(42, 'FirstName_42', 'LastName_42', 85000, 2),
(43, 'FirstName_43', 'LastName_43', 62000, 3),
(44, 'FirstName_44', 'LastName_44', 94000, 4),
(45, 'FirstName_45', 'LastName_45', 53000, 5),
(46, 'FirstName_46', 'LastName_46', 68000, 1),
(47, 'FirstName_47', 'LastName_47', 102000, 2),
(48, 'FirstName_48', 'LastName_48', 59000, 3),
(49, 'FirstName_49', 'LastName_49', 87000, 4),
(50, 'FirstName_50', 'LastName_50', 72000, 5);

-- Insert data into the projects table
INSERT INTO projects (id, title, start_date, end_date, budget) VALUES
(1, 'Project_1', '2017-03-01', '2017-08-01', 50000),
(2, 'Project_2', '2018-05-10', '2018-11-20', 75000),
(3, 'Project_3', '2017-07-15', '2017-12-10', 60000),
(4, 'Project_4', '2018-01-20', '2018-06-30', 80000),
(5, 'Project_5', '2017-09-05', '2018-02-10', 90000),
(6, 'Project_6', '2018-03-15', '2018-09-25', 40000),
(7, 'Project_7', '2017-11-01', '2018-04-15', 55000),
(8, 'Project_8', '2017-02-12', '2017-07-30', 30000),
(9, 'Project_9', '2018-04-05', '2018-10-20', 85000),
(10, 'Project_10', '2017-06-15', '2017-12-30', 70000);

-- Insert data into the employees_projects table
INSERT INTO employees_projects (id, project_id, employee_id) VALUES
(1, 1, 1),
(2, 2, 2),
(3, 3, 3),
(4, 4, 4),
(5, 5, 5),
(6, 6, 6),
(7, 7, 7),
(8, 8, 8),
(9, 9, 9),
(10, 10, 10),
(11, 1, 11),
(12, 2, 12),
(13, 3, 13),
(14, 4, 14),
(15, 5, 15),
(16, 6, 16),
(17, 7, 17),
(18, 8, 18),
(19, 9, 19),
(20, 10, 20),
(21, 1, 21),
(22, 2, 22),
(23, 3, 23),
(24, 4, 24),
(25, 5, 25),
(26, 6, 26),
(27, 7, 27),
(28, 8, 28),
(29, 9, 29),
(30, 10, 30);


===========================================================================================================================================================================================


/*
Return count of projects per department name
*/
select d.name as department_name 

from EMPLOYEES e
Inner Join DEPARTMENTS d
on e.id = d.id 









/*
Return average projects per employee for each department
*/








/*
Return first and last name of employees without a project
*/








/*
Return highest budget project for each employee (employee name, project title, project budget)
*/










/*
Return average budget for projects starting in each month, 2017-2018, and percentage change (formatted to 2 decimal places) vs prior month 
*/



 



