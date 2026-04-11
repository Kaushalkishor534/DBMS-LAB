# EXPERIMENT-7: 
## Q1. Compute the number of days remaining in this year.
```sql
SELECT DATEDIFF(
       CONCAT(YEAR(CURDATE()), '-12-31'),
       CURDATE()
) AS REMAINING_DAYS;
```
**OUTPUT:**
```
+----------------+
| REMAINING_DAYS |
+----------------+
|            309 |
+----------------+
1 row in set (0.000 sec)
```
## Q2. Find the highest salary, lowest salary, and the difference between them.
```sql
MariaDB [Archisha]> SELECT MAX(SAL) AS MAX_SALARY,
    -> MIN(SAL) AS MIN_SALARY,
    -> MAX(SAL) - MIN(SAL) AS SALARY_DIFF
    -> FROM EMPLOYEE;
```
**OUTPUT:**
```
+------------+------------+-------------+
| MAX_SALARY | MIN_SALARY | SALARY_DIFF |
+------------+------------+-------------+
|       6050 |        968 |        5082 |
+------------+------------+-------------+
1 row in set (0.092 sec)
```
## Q3. List employees whose commission is greater than 25% of their salary.
``` sql

MariaDB [Archisha]> SELECT ENAME, SAL, COMM
    -> FROM EMPLOYEE
    -> WHERE COMM > (0.25 * SAL);
 ```
**OUTPUT:**
```
+--------+------+------+
| ENAME  | SAL  | COMM |
+--------+------+------+
| MARTIN | 1250 | 1400 |
+--------+------+------+
1 row in set (0.000 sec)
```
## Q4. Display salary in dollar format.
``` sql
MariaDB [Archisha]> SELECT ENAME,
    -> CONCAT('$', FORMAT(SAL,2)) AS SALARY
    -> FROM EMPLOYEE;
```
**OUTPUT:**
```
+--------+-----------+
| ENAME  | SALARY    |
+--------+-----------+
| SMITH  | $968.00   |
| ALLEN  | $1,600.00 |
| WARD   | $1,250.00 |
| JONES  | $3,600.00 |
| MARTIN | $1,250.00 |
| BLAKE  | $3,449.00 |
| CLARK  | $2,965.00 |
| SCOTT  | $3,630.00 |
| KING   | $6,050.00 |
| TURNER | $1,650.00 |
| ADAMS  | $1,331.00 |
| JAMES  | $1,150.00 |
| FORD   | $3,630.00 |
| MILLER | $1,573.00 |
+--------+-----------+
14 rows in set (0.052 sec)
```
## Q5.Create a matrix query to display the job, salary for that job based on department number, and total salary for that job across departments.
```sql
MariaDB [Archisha]> SELECT JOB,
    -> SUM(CASE DEPTNO WHEN 10 THEN SAL ELSE 0 END) AS DEPT10,
    -> SUM(CASE DEPTNO WHEN 10 THEN SAL ELSE 0 END) AS DEPT20,
    -> SUM(CASE DEPTNO WHEN 10 THEN SAL ELSE 0 END) AS DEPT30,
    -> SUM(CASE DEPTNO WHEN 10 THEN SAL ELSE 0 END) AS DEPT40,
    -> SUM(SAL) AS TOTAL_SALARY
    -> FROM EMPLOYEE
    -> GROUP BY JOB;
```
**OUTPUT:**
```
+-----------+--------+--------+--------+--------+--------------+
| JOB       | DEPT10 | DEPT20 | DEPT30 | DEPT40 | TOTAL_SALARY |
+-----------+--------+--------+--------+--------+--------------+
| ANALYST   |      0 |      0 |      0 |      0 |         7260 |
| CLERK     |   1573 |   1573 |   1573 |   1573 |         5022 |
| MANAGER   |      0 |      0 |      0 |      0 |        10014 |
| PRESIDENT |      0 |      0 |      0 |      0 |         6050 |
| SALESMAN  |      0 |      0 |      0 |      0 |         5750 |
+-----------+--------+--------+--------+--------+--------------+
5 rows in set (0.001 sec)

```
## Q6. Display the total number of employees and the number hired in 1980, 1981, 1982, and 1983.
```sql
MariaDB [Archisha]> SELECT COUNT(*) AS TOTAL_EMPLOYEES,
    -> SUM(CASE WHEN YEAR(HIREDATE)=1980 THEN 1 ELSE 0 END) AS "YEAR1980",
    -> SUM(CASE WHEN YEAR(HIREDATE)=1981 THEN 1 ELSE 0 END) AS "YEAR1981",
    -> SUM(CASE WHEN YEAR(HIREDATE)=1982 THEN 1 ELSE 0 END) AS "YEAR1982",
    -> SUM(CASE WHEN YEAR(HIREDATE)=1983 THEN 1 ELSE 0 END) AS "YEAR1983"
    -> FROM EMPLOYEE;
```
**OUTPUT:**
```
+-----------------+----------+----------+----------+----------+
| TOTAL_EMPLOYEES | YEAR1980 | YEAR1981 | YEAR1982 | YEAR1983 |
+-----------------+----------+----------+----------+----------+
|              14 |        1 |       10 |        2 |        1 |
+-----------------+----------+----------+----------+----------+
1 row in set (0.011 sec)
```
## Q7. Write a query to get the last Sunday of the current month.
```sql
MariaDB [Archisha]> SELECT DATE_SUB(
    ->  LAST_DAY(CURDATE()),
    -> INTERVAL (WEEKDAY(LAST_DAY(CURDATE())) + 1) DAY
    -> ) AS LAST_SUNDAY;
```
**OUTPUT:**
```
+-------------+
| LAST_SUNDAY |
+-------------+
| 2026-02-22  |
+-------------+
1 row in set (0.000 sec)
```
## Q8.Display department numbers and total number of employees working in each department.
```sql
MariaDB [Archisha]> SELECT DEPTNO, COUNT(*) AS TOTAL_EMPLOYEES
    -> FROM EMPLOYEE
    -> GROUP BY DEPTNO
    -> ORDER BY DEPTNO;
```
**OUTPUT:**
```
+--------+-----------------+
| DEPTNO | TOTAL_EMPLOYEES |
+--------+-----------------+
|     10 |               1 |
|     20 |               6 |
|     30 |               6 |
|     40 |               1 |
+--------+-----------------+
4 rows in set (0.011 sec)
```
## Q9. Display various jobs and total number of employees within each job group.
``` sql
MMariaDB [Archisha]> SELECT JOB, COUNT(*) AS TOTAL_EMPLOYEES
    -> FROM EMPLOYEE
    -> GROUP BY JOB;
```
**OUTPUT:**
```
+-----------+-----------------+
| JOB       | TOTAL_EMPLOYEES |
+-----------+-----------------+
| ANALYST   |               2 |
| CLERK     |               4 |
| MANAGER   |               3 |
| PRESIDENT |               1 |
| SALESMAN  |               4 |
+-----------+-----------------+
5 rows in set (0.001 sec)
```
## Q10. Display department numbers and total salary for each department.
```sql
MariaDB [Archisha]> SELECT DEPTNO, SUM(SAL) AS TOTAL_SALARY
    -> FROM EMPLOYEE
    -> GROUP BY DEPTNO;
```
**OUTPUT:**
```
+--------+--------------+
| DEPTNO | TOTAL_SALARY |
+--------+--------------+
|     10 |         1573 |
|     20 |        18544 |
|     30 |        10349 |
|     40 |         3630 |
+--------+--------------+
4 rows in set (0.000 sec)
```
