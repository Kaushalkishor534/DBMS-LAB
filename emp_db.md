## Question 1:
---
### creation of database
```sql
MariaDB [(none)]> CREATE DATABASE emp;
Query OK, 1 row affected (0.003 sec)
MariaDB [(none)]> USE emp;
Database changed
```
### creation of department table
```sql
MariaDB [emp]> CREATE TABLE DEPARTMENT(
    -> DEPT_NO INT(4) PRIMARY KEY,
    -> Dname VARCHAR(15) NOT NULL
    -> );
Query OK, 0 rows affected (0.017 sec)
```
### creation of employee table
```sql
MariaDB [emp]> CREATE TABLE EMPLOYEE (
    -> Empno INT PRIMARY KEY,
    -> Ename VARCHAR(20) NOT NULL,
    -> job VARCHAR(20),
    ->  Mgr INT(4),
    -> Hiredate Date,
    -> Sal INT(10),
    -> Comm INT,
    -> Deptno INT,
    -> FOREIGN KEY (Deptno) REFERENCES DEPARTMENT(DEPT_NO)
    -> );
Query OK, 0 rows affected (0.053 sec)
```
### filling values in department table
```sql
MariaDB [emp]> INSERT INTO DEPARTMENT VALUES (10, 'RESEARCH'),(20, 'ACCOUNTING'),(30, 'SALES'), (40, 'OPERATIONS');
Query OK, 1 row affected (0.002 sec)
```
### filling values in employee table
```sql
MariaDB [emp]> INSERT INTO EMPLOYEE VALUES (7369,'SMITH','CLERK',7902,DATE '1980-12-17',800,NULL,20),(7499,'ALLEN','SALESMAN',7698,DATE '1981-02-20',1600,300,30),(7521,'WARD','SALESMAN',7698,DATE '1981-02-22',1250,300,30),(7566,'JONES','MANAGER',7839,DATE '1981-04-02',2975,NULL,20),(7654,'MARTIN','SALESMAN',7698,DATE '1981-09-28',1250,1400,30),(7698,'BLAKE','MANAGER',7839,DATE '1981-05-01',2850,NULL,30),(7782,'CLARK','MANAGER',7839,DATE '1981-06-09',2450,NULL,20),(7788,'SCOTT','ANALYST',7566,DATE '1982-12-09',3000,NULL,40),(7839,'KING','PRESIDENT',NULL,DATE '1981-11-17',5000,NULL,20),(7844,'TURNER','SALESMAN',7698,DATE '1981-09-08',1500,0,30),(7876,'ADAMS','CLERK',7788,DATE '1983-01-12',1100,NULL,20),(7900,'JAMES','CLERK',7698,DATE '1981-12-03',950,NULL,30), (7902,'FORD','ANALYST',7566,DATE '1981-12-03',3000,NULL,20),(7934,'MILLER','CLERK',7782,DATE '1982-01-23',1300,NULL,10);
Query OK, 1 row affected (0.002 sec)
```
### Create EMPLOYEE_MASTER table with data using EMPLOYEE table
```sql
MariaDB [emp]> CREATE TABLE EMPLOYEE_MASTER AS
    -> SELECT * FROM EMPLOYEE;
Query OK, 14 rows affected (0.040 sec)
Records: 14  Duplicates: 0  Warnings: 0
```
### Delete all records from EMPLOYEE_MASTER whose DEPTNO = 10
```sql
MariaDB [emp]> DELETE FROM EMPLOYEE_MASTER
    -> WHERE DEPTNO = 10;
Query OK, 1 row affected (0.019 sec)
```
### Alter SAL column size to 10,2
```sql
MariaDB [emp]> UPDATE EMPLOYEE_MASTER
    -> SET SAL = SAL + (SAL * 0.10)
    -> WHERE DEPTNO = 20;
Query OK, 6 rows affected (0.020 sec)
Rows matched: 6  Changed: 6  Warnings: 0
```
## Question 2:
---
### 1.List all dystinct jobs in employee
```sql 
MariaDB [EMP]> SELECT DISTINCT job FROM employee;
+-----------+
| job       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.001 sec)
```
### 2.All info about deptno=30 in employee
```sql
MariaDB [EMP]> SELECT * FROM employee
    -> WHERE Deptno=30;
+-------+--------+----------+------+------------+------+------+--------+
| Empno | Ename  | job      | Mgr  | Hiredate   | Sal  | Comm | Deptno |
+-------+--------+----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+--------+----------+------+------------+------+------+--------+
6 rows in set (0.018 sec)
```
### 3.find all department no. with department name greater than 20.
```sql
MariaDB [EMP]> SELECT job,Deptno
    -> FROM employee WHERE
    -> Deptno>20;
+----------+--------+
| job      | Deptno |
+----------+--------+
| SALESMAN |     30 |
| SALESMAN |     30 |
| SALESMAN |     30 |
| MANAGER  |     30 |
| ANALYST  |     40 |
| SALESMAN |     30 |
| CLERK    |     30 |
+----------+--------+
7 rows in set (0.001 sec)
```
### 4.Find All informatiom about all managers as well as clerks in department 30.
```sql
MariaDB [EMP]> SELECT * FROM employee
    -> WHERE job in ('MANAGER','CLERKS') AND Deptno=30;
+-------+-------+---------+------+------------+------+------+--------+
| Empno | Ename | job     | Mgr  | Hiredate   | Sal  | Comm | Deptno |
+-------+-------+---------+------+------------+------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 2850 | NULL |     30 |
+-------+-------+---------+------+------------+------+------+--------+
1 row in set (0.002 sec)
```
### 5.list employee name,employee number and department of all clerks.
```sql
MariaDB [EMP]> SELECT Ename,Empno,job FROM employee
    -> WHERE job= 'CLERK';
+--------+-------+-------+
| Ename  | Empno | job   |
+--------+-------+-------+
| SMITH  |  7369 | CLERK |
| ADAMS  |  7876 | CLERK |
| JAMES  |  7900 | CLERK |
| MILLER |  7934 | CLERK |
+--------+-------+-------+
```
### 6.All managers not in department 30.
```sql
MariaDB [EMP]> SELECT * FROM employee
    -> where job='MANAGER'AND Deptno <> 30;
+-------+-------+---------+------+------------+------+------+--------+
| Empno | Ename | job     | Mgr  | Hiredate   | Sal  | Comm | Deptno |
+-------+-------+---------+------+------------+------+------+--------+
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 | 2975 | NULL |     20 |
|  7782 | CLARK | MANAGER | 7839 | 1981-06-09 | 2450 | NULL |     20 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
```
### 7.Informattion about all employees in department 10 who are not managers or clerk.
```sql 
MariaDB [EMP]> SELECT * FROM employee
    -> WHERE Deptno=10 AND job NOT IN ('MANAGERS','CLERK');
Empty set (0.001 sec)
```
### 8.employeess and jobs earning between 1200 and 1400.
```sql
MariaDB [EMP]> SELECT * FROM employee
    -> WHERE Sal BETWEEN 1200 AND 1400;
+-------+--------+----------+------+------------+------+------+--------+
| Empno | Ename  | job      | Mgr  | Hiredate   | Sal  | Comm | Deptno |
+-------+--------+----------+------+------------+------+------+--------+
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7934 | MILLER | CLERK    | 7782 | 1982-01-23 | 1300 | NULL |     10 |
+-------+--------+----------+------+------------+------+------+--------+
3 rows in set (0.001 sec)
```
### 9.Name and department number of employee who are clerk,analyst or salesman.
```sql
MariaDB [EMP]> SELECT Ename,Deptno FROM employee
    -> WHERE job IN ('CLERK','ANALYST','SALESMAN');
+--------+--------+
| Ename  | Deptno |
+--------+--------+
| SMITH  |     20 |
| ALLEN  |     30 |
| WARD   |     30 |
| MARTIN |     30 |
| SCOTT  |     40 |
| TURNER |     30 |
| ADAMS  |     20 |
| JAMES  |     30 |
| FORD   |     20 |
| MILLER |     10 |
+--------+--------+
10 rows in set (0.001 sec)
```
### 10. Name and Department number of employee whose names start with m.
```sql
MariaDB [EMP]> SELECT Ename,Deptno FROM employee
    -> WHERE Ename LIKE 'M%';
+--------+--------+
| Ename  | Deptno |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+
2 rows in set (0.001 sec)
```
## Question 3:
### 1.list employees and jobs in department 30 in descending order by salary.
```sql
MariaDB [EMP]> SELECT Ename,job FROM employee
    -> WHERE Deptno=30 ORDER BY Sal;
+--------+----------+
| Ename  | job      |
+--------+----------+
| JAMES  | CLERK    |
| WARD   | SALESMAN |
| MARTIN | SALESMAN |
| TURNER | SALESMAN |
| ALLEN  | SALESMAN |
| BLAKE  | MANAGER  |
+--------+----------+
6 rows in set (0.002 sec)
```
### 2.list job and department no of employees whose name has five leeters long begin with a and end with n.
```sql
MariaDB [EMP]> SELECT job,Deptno FROM employee
    -> WHERE Ename='a___n';
Empty set (0.001 sec)
```
### 3.Display name of employees whoses name start with 's'.
```sql
MariaDB [EMP]> SELECT Ename FROM employee
    -> WHERE Ename LIKE 'S%';
+-------+
| Ename |
+-------+
| SMITH |
| SCOTT |
+-------+
2 rows in set (0.001 sec)
```
### 4.Name of employees ending with 's'.
```sql
MariaDB [EMP]> SELECT Ename FROM employee
    -> WHERE Ename LIKE '%S';
+-------+
| Ename |
+-------+
| JONES |
| ADAMS |
| JAMES |
+-------+
3 rows in set (0.001 sec)
```
### 5. Name of employee working in department 10 or 20 or 40 or employees working as clerks,salesman,analyst.
```sql
MariaDB [EMP]> SELECT Ename FROM employee
    -> WHERE Deptno IN (10,20,40) AND job IN('CLERK','SALESMAN','ANALYST');
    +--------+
| Ename  |
+--------+
| SMITH  |
| SCOTT  |
| ADAMS  |
| FORD   |
| MILLER |
+--------+
5 rows in set (0.001 sec)
```
### 6.Employee no. and names for employees earns comission.
```sql
MariaDB [EMP]> SELECT Ename FROM employee
    -> WHERE Comm IS NOT NULL AND Comm <> 0;
+--------+
| Ename  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
+--------+
3 rows in set (0.005 sec)
```
### 7.employee no. with their total salary.
```sql
MariaDB [EMP]> SELECT Empno,(Sal+IFNULL(Comm,0)) AS Total_salary
    -> FROM employee;
+-------+--------------+
| Empno | Total_salary |
+-------+--------------+
|  7369 |          800 |
|  7499 |         1900 |
|  7521 |         1550 |
|  7566 |         2975 |
|  7654 |         2650 |
|  7698 |         2850 |
|  7782 |         2450 |
|  7788 |         3000 |
|  7839 |         5000 |
|  7844 |         1500 |
|  7876 |         1100 |
|  7900 |          950 |
|  7902 |         3000 |
|  7934 |         1300 |
+-------+--------------+
14 rows in set (0.001 sec)
```
### 8.employee no. with annual salary.
```sql
MariaDB [EMP]> SELECT Empno,(Sal*12) AS Annual_salary
    -> FROM employee;
+-------+---------------+
| Empno | Annual_salary |
+-------+---------------+
|  7369 |          9600 |
|  7499 |         19200 |
|  7521 |         15000 |
|  7566 |         35700 |
|  7654 |         15000 |
|  7698 |         34200 |
|  7782 |         29400 |
|  7788 |         36000 |
|  7839 |         60000 |
|  7844 |         18000 |
|  7876 |         13200 |
|  7900 |         11400 |
|  7902 |         36000 |
|  7934 |         15600 |
+-------+---------------+
14 rows in set (0.001 sec)
```
### 9.Names of employees working as clerks and salary more than  3,000.
```sql
MariaDB [EMP]> SELECT Ename FROM employee
    -> WHERE job IN ('CLERK') AND Sal>3000;
Empty set (0.018 sec)
```
### 10.Names of employees working as clerk,salesman or analyst and salary more than 3000.
```sql
MariaDB [EMP]> SELECT Ename FROM employee
    -> WHERE job IN ('CLERK','SALESMAN','ANALYST') AND
    -> Sal>3000;
Empty set (0.001 sec)
```
---