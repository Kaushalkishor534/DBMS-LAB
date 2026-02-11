# PPRACTICAL QUESTION - 2 :-
---
## 1.List all distinct job in employee.
```sql
MariaDB [kaushal]> select distinct job from employee;
+-----------+
| job       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.003 sec)
```
## 2.All info about employees in dept no=30.
```sql
MariaDB [kaushal]> select * from employee
    -> where deptno=30;
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
6 rows in set (0.019 sec)
```
## 3.find dept no. greater than dept no. = 20.
```sql
MariaDB [kaushal]> select * from employee
    -> where deptno>20;;
+-------+--------+----------+------+------------+------+------+--------+
| Empno | Ename  | job      | Mgr  | Hiredate   | Sal  | Comm | Deptno |
+-------+--------+----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7788 | SCOTT  | ANALYST  | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+--------+----------+------+------------+------+------+--------+
7 rows in set (0.002 sec)
```
## 4. All info about managers,clerk in dept no 30.
```sql
MariaDB [kaushal]> select * from employee
    -> where job in ('MANAGER','CLERK') AND DEPTNO=30;
+-------+-------+---------+------+------------+------+------+--------+
| Empno | Ename | job     | Mgr  | Hiredate   | Sal  | Comm | Deptno |
+-------+-------+---------+------+------------+------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
```
## 5.EMPLOYEE name ,employee number and department of all clerk.
```sql
MariaDB [kaushal]> select ename,empno,deptno from employee
    -> where job ='CLERK';
+--------+-------+--------+
| ename  | empno | deptno |
+--------+-------+--------+
| SMITH  |  7369 |     20 |
| ADAMS  |  7876 |     20 |
| JAMES  |  7900 |     30 |
| MILLER |  7934 |     10 |
+--------+-------+--------+
4 rows in set (0.001 sec)
```
## 6.Managers not in dept no. 20.
```sql
MariaDB [kaushal]> select ename from employee
    -> where deptno <> 20 and job ="MANAGER"
    -> ;
+-------+
| ename |
+-------+
| BLAKE |
+-------+
1 row in set (0.018 sec)
```
## 7.All info about all employee in deptno.10 who are not mangers or clerk.
```sql

MariaDB [kaushal]> select * from employee
    -> where deptno=10 and job not in ('MANAGER','CLERK');
Empty set (0.001 sec)
```
## 8.EMPLOYEE EARNING BETWEEN 1200 TO 1400.
```SQL
MariaDB [kaushal]> SELECT ENAME FROM EMPLOYEE
    -> WHERE SAL BETWEEN 1200 AND 1400;
+--------+
| ENAME  |
+--------+
| WARD   |
| MARTIN |
| MILLER |
+--------+
3 rows in set (0.001 sec)
```
## 9.NAME AND EMPNO. OF EMPLOYEE WHO ARE CLERK,ANALYST,SALESMAN.
```SQL

MariaDB [kaushal]> SELECT ENAME,DEPTNO FROM EMPLOYEE
    -> WHERE JOB IN ('CLERK','ANALYST','SALESMAN');
+--------+--------+
| ENAME  | DEPTNO |
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
## 10.NAME AND DEPT NO. OF EMPLOYEES WHOSE NAMES BEGAN WITH 'M'.
```SQL
MariaDB [kaushal]> SELECT ENAME FROM EMPLOYEE
    -> WHERE ENAME LIKE 'M%';
+--------+
| ENAME  |
+--------+
| MARTIN |
| MILLER |
+--------+
2 rows in set (0.001 sec)
```
---
---