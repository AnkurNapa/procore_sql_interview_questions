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



 



