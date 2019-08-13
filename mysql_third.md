
**作业**

### 项目十: 各部门工资最高的员工（难度：中等）
```
创建Employee 表，包含所有员工信息，每个员工有其对应的 Id, salary 和 department Id。
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
创建Department 表，包含公司所有部门的信息。
+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+
编写一个 SQL 查询，找出每个部门工资最高的员工。例如，根据上述给定的表格，Max 在 IT 部门有最高工资，Henry 在 Sales 部门有最高工资。
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| Sales      | Henry    | 80000  |
+------------+----------+--------+
​```
```

## 解答:
```mysql
USE demo;
CREATE TABLE employee ( id INT UNSIGNED PRIMARY KEY auto_increment, NAME VARCHAR ( 50 ) NOT NULL, salary INT NOT NULL, departmentid INT NOT NULL );
CREATE TABLE department ( id INT UNSIGNED PRIMARY KEY auto_increment, NAME VARCHAR ( 50 ) NOT NULL );
INSERT INTO employee ( NAME, salary, departmentid )
VALUES
	( 'Joe', '70000', '1' ),
	( 'Henry', '80000', '2' ),
	( 'Sam', '60000', '2' ),
	( 'Max', '90000', '1' );
INSERT INTO department
VALUES
	( '1', 'IT' ),
	( '2', 'Sales' );

SELECT
	Department.NAME AS Department,
	Employee.NAME AS Employee,
	Salary 
FROM
	Employee
	JOIN Department ON Employee.DepartmentId = Department.Id 
WHERE
	( Employee.DepartmentId, Salary ) IN ( SELECT DepartmentId, MAX( Salary ) FROM Employee GROUP BY DepartmentId )
```