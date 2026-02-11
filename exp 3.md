# PRACTICAL QUESTION -3 :-
---
## 1. ALL EMPLOYEES AND JOBS IN DEPT 30 IN DEESCENDING ORDER BY SALARY.
```SQL
MariaDB [kaushal]> SELECT ENAME,JOB,SAL FROM EMPLOYEE
    -> WHERE DEPTNO = 30 ORDER BY SAL DESC;
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| BLAKE  | MANAGER  | 2850 |
| ALLEN  | SALESMAN | 1600 |
| TURNER | SALESMAN | 1500 |
| WARD   | SALESMAN | 1250 |
| MARTIN | SALESMAN | 1250 |
| JAMES  | CLERK    |  950 |
+--------+----------+------+
6 rows in set (0.001 sec)
```
---
## 2. NAME And deptno for names having five characters begin with "a" and end with " n".
```sql
MariaDB [kaushal]> select ename,deptno from employee
    -> where ename like "a___n";
+-------+--------+
| ename | deptno |
+-------+--------+
| ALLEN |     30 |
+-------+--------+
1 row in set (0.001 sec)
```
---
## 3. Names starts with 's'.
```sql
MariaDB [kaushal]> select ename from employee
    -> where ename like 's%';
+-------+
| ename |
+-------+
| SMITH |
| SCOTT |
+-------+
2 rows in set (0.001 sec)
```
---
## 4. Name of employee name ending with 's'.
```sql
MariaDB [kaushal]> select ename from employee
    -> where ename like '%s';
+-------+
| ename |
+-------+
| JONES |
| ADAMS |
| JAMES |
+-------+
3 rows in set (0.001 sec)
```
---
## 5. Name of employees working in dept 20,30,40 or working as clerk or analyst or salesman.
```sql
MariaDB [kaushal]> select ename from employee
    -> where job in ('clerk','analyst','salesman')
    -> or deptno in (10,20,40);
+--------+
| ename  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| JAMES  |
| FORD   |
| MILLER |
+--------+
13 rows in set (0.001 sec)
```
---
## 6. Display names of employees who earms commission.
```sql

MariaDB [kaushal]> select ename from employee
    -> where comm is not null;
+--------+
| ename  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| TURNER |
+--------+
4 rows in set (0.001 sec)
```
---
## 7. Display total salary and emp no. of employees.
```sql
MariaDB [kaushal]> select empno,(sal+ifnull(comm,0)) as total_salary
    -> from employee;
+-------+--------------+
| empno | total_salary |
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
---
## 8. Display annual salary of employees with emp no.
```sql
MariaDB [kaushal]> select empno,(sal*12) as annual_salary
    -> from employee;
+-------+---------------+
| empno | annual_salary |
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
---
## 9. Display employees working as clerk and drawing salary of 3000.
```sql
MariaDB [kaushal]> select ename from employee
    -> where job ='clerk' AND sal>3000;
Empty set (0.001 sec)

```
---
## 10. Display employees working as clerk or salesman,analyst and drawing salary of 3000.
```sql
MariaDB [kaushal]> select ename from employee
    -> where job in ('clerk','salesman','analyst') AND sal>3000;
Empty set (0.001 sec)
```
----
---