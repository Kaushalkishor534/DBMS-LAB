
# Experiment8

## 1. Display all employees with their dept name.
```sql
MariaDB [kaushal]> SELECT E.EMPNO, E.ENAME, D.DNAME
    -> FROM EMPLOYEE E
    -> JOIN DEPARTMENT D
    -> ON E.DEPTNO = D.DEPTNO;
+-------+--------+------------+
| EMPNO | ENAME  | DNAME      |
+-------+--------+------------+
|  7369 | SMITH  | ACCOUNTING |
|  7499 | ALLEN  | SALES      |
|  7521 | WARD   | SALES      |
|  7566 | JONES  | ACCOUNTING |
|  7654 | MARTIN | SALES      |
|  7698 | BLAKE  | SALES      |
|  7782 | CLARK  | ACCOUNTING |
|  7788 | SCOTT  | ACCOUNTING |
|  7839 | KING   | ACCOUNTING |
|  7844 | TURNER | SALES      |
|  7876 | ADAMS  | ACCOUNTING |
|  7900 | JAMES  | SALES      |
|  7902 | FORD   | ACCOUNTING |
|  7934 | MILLER | RESEARCH   |
+-------+--------+------------+
14 rows in set (0.011 sec)
```

## 2. Display those employees whose manager names is jones, and also display their manager name.
```sql
MariaDB [kaushal]> SELECT
    ->     E.ENAME AS EMPLOYEE,
    ->     M.ENAME AS MANAGER
    -> FROM EMPLOYEE E
    -> JOIN EMPLOYEE M
    -> ON E.MGR = M.EMPNO
    -> WHERE M.ENAME = 'JONES';
+----------+---------+
| EMPLOYEE | MANAGER |
+----------+---------+
| SCOTT    | JONES   |
| FORD     | JONES   |
+----------+---------+
2 rows in set (0.009 sec)
```

## 3. Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.
```sql
MariaDB [kaushal]> SELECT e.ENAME, e.JOB, d.DNAME, m.ENAME AS MANAGER, s.GRADE
    -> FROM EMPLOYEE e
    -> JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
    -> LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO
    -> JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
    -> ORDER BY d.DNAME;
+--------+-----------+------------+---------+-------+
| ENAME  | JOB       | DNAME      | MANAGER | GRADE |
+--------+-----------+------------+---------+-------+
| CLARK  | MANAGER   | ACCOUNTING | KING    | D     |
| SCOTT  | ANALYST   | ACCOUNTING | JONES   | E     |
| FORD   | ANALYST   | ACCOUNTING | JONES   | E     |
| JONES  | MANAGER   | ACCOUNTING | KING    | E     |
| KING   | PRESIDENT | ACCOUNTING | NULL    | E     |
| SMITH  | CLERK     | ACCOUNTING | FORD    | A     |
| ADAMS  | CLERK     | ACCOUNTING | SCOTT   | B     |
| MILLER | CLERK     | RESEARCH   | CLARK   | C     |
| JAMES  | CLERK     | SALES      | BLAKE   | A     |
| WARD   | SALESMAN  | SALES      | BLAKE   | B     |
| MARTIN | SALESMAN  | SALES      | BLAKE   | B     |
| TURNER | SALESMAN  | SALES      | BLAKE   | C     |
| BLAKE  | MANAGER   | SALES      | KING    | E     |
| ALLEN  | SALESMAN  | SALES      | BLAKE   | C     |
+--------+-----------+------------+---------+-------+
14 rows in set (0.007 sec)
```

## 4. List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.
```sql
MariaDB [kaushal]> SELECT e.ENAME, e.JOB, e.SAL, s.GRADE, d.DNAME
    -> FROM EMPLOYEE e
    -> JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
    -> JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
    -> WHERE e.JOB <> 'CLERK'
    -> ORDER BY e.SAL DESC;
+--------+-----------+---------+-------+------------+
| ENAME  | JOB       | SAL     | GRADE | DNAME      |
+--------+-----------+---------+-------+------------+
| KING   | PRESIDENT | 5500.00 | E     | ACCOUNTING |
| FORD   | ANALYST   | 3300.00 | E     | ACCOUNTING |
| SCOTT  | ANALYST   | 3300.00 | E     | ACCOUNTING |
| JONES  | MANAGER   | 3272.50 | E     | ACCOUNTING |
| BLAKE  | MANAGER   | 3135.00 | E     | SALES      |
| CLARK  | MANAGER   | 2695.00 | D     | ACCOUNTING |
| ALLEN  | SALESMAN  | 1600.00 | C     | SALES      |
| TURNER | SALESMAN  | 1500.00 | C     | SALES      |
| MARTIN | SALESMAN  | 1250.00 | B     | SALES      |
| WARD   | SALESMAN  | 1250.00 | B     | SALES      |
+--------+-----------+---------+-------+------------+
10 rows in set (0.001 sec)
```

## 5. Display employee name, his job and his manager. Display also employees who are without manager.
```sql
MariaDB [kaushal]> SELECT e.ENAME, e.JOB, m.ENAME AS MANAGER
    -> FROM EMPLOYEE e
    -> LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO;
+--------+-----------+---------+
| ENAME  | JOB       | MANAGER |
+--------+-----------+---------+
| SMITH  | CLERK     | FORD    |
| ALLEN  | SALESMAN  | BLAKE   |
| WARD   | SALESMAN  | BLAKE   |
| JONES  | MANAGER   | KING    |
| MARTIN | SALESMAN  | BLAKE   |
| BLAKE  | MANAGER   | KING    |
| CLARK  | MANAGER   | KING    |
| SCOTT  | ANALYST   | JONES   |
| KING   | PRESIDENT | NULL    |
| TURNER | SALESMAN  | BLAKE   |
| ADAMS  | CLERK     | SCOTT   |
| JAMES  | CLERK     | BLAKE   |
| FORD   | ANALYST   | JONES   |
| MILLER | CLERK     | CLARK   |
+--------+-----------+---------+
14 rows in set (0.001 sec)
```

## 6. List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.
```sql
MariaDB [kaushal]> SELECT e.ENAME, e.JOB, (e.SAL * 12) AS ANNUAL_SAL,
    ->        e.DEPTNO, d.DNAME, s.GRADE
    -> FROM EMPLOYEE e
    -> JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
    -> JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
    -> WHERE (e.SAL * 12) >= 36000
    ->    OR e.JOB <> 'CLERK';
+--------+-----------+------------+--------+------------+-------+
| ENAME  | JOB       | ANNUAL_SAL | DEPTNO | DNAME      | GRADE |
+--------+-----------+------------+--------+------------+-------+
| ALLEN  | SALESMAN  |   19200.00 |     30 | SALES      | C     |
| WARD   | SALESMAN  |   15000.00 |     30 | SALES      | B     |
| JONES  | MANAGER   |   39270.00 |     20 | ACCOUNTING | E     |
| MARTIN | SALESMAN  |   15000.00 |     30 | SALES      | B     |
| BLAKE  | MANAGER   |   37620.00 |     30 | SALES      | E     |
| CLARK  | MANAGER   |   32340.00 |     20 | ACCOUNTING | D     |
| SCOTT  | ANALYST   |   39600.00 |     20 | ACCOUNTING | E     |
| KING   | PRESIDENT |   66000.00 |     20 | ACCOUNTING | E     |
| TURNER | SALESMAN  |   18000.00 |     30 | SALES      | C     |
| FORD   | ANALYST   |   39600.00 |     20 | ACCOUNTING | E     |
+--------+-----------+------------+--------+------------+-------+
10 rows in set (0.001 sec)
```

## 7. List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.
```sql
MariaDB [kaushal]> SELECT e.ENAME, e.JOB, (e.SAL * 12) AS ANNUAL_SAL,
    ->        e.DEPTNO, d.DNAME, s.GRADE
    -> FROM EMPLOYEE e
    -> JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
    -> JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
    -> WHERE (e.SAL * 12) = 30000
    ->   AND e.JOB <> 'CLERK';
Empty set (0.001 sec)
```

## 8. List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager.
```sql
MariaDB [kaushal]> SELECT
    ->     e.EMPNO,
    ->     e.ENAME,
    ->     IFNULL(CAST(m.EMPNO AS CHAR), 'No Manager') AS MGR_NO,
    ->     IFNULL(m.ENAME, 'No Manager') AS MGR_NAME
    -> FROM EMPLOYEE e
    -> LEFT JOIN EMPLOYEE m
    -> ON e.MGR = m.EMPNO;
+-------+--------+------------+------------+
| EMPNO | ENAME  | MGR_NO     | MGR_NAME   |
+-------+--------+------------+------------+
|  7369 | SMITH  | 7902       | FORD       |
|  7499 | ALLEN  | 7698       | BLAKE      |
|  7521 | WARD   | 7698       | BLAKE      |
|  7566 | JONES  | 7839       | KING       |
|  7654 | MARTIN | 7698       | BLAKE      |
|  7698 | BLAKE  | 7839       | KING       |
|  7782 | CLARK  | 7839       | KING       |
|  7788 | SCOTT  | 7566       | JONES      |
|  7839 | KING   | No Manager | No Manager |
|  7844 | TURNER | 7698       | BLAKE      |
|  7876 | ADAMS  | 7788       | SCOTT      |
|  7900 | JAMES  | 7698       | BLAKE      |
|  7902 | FORD   | 7566       | JONES      |
|  7934 | MILLER | 7782       | CLARK      |
+-------+--------+------------+------------+
14 rows in set (0.001 sec)
```

## 9. Select dept name, dept no and sum of sal.
```sql
MariaDB [kaushal]> SELECT d.DEPTNO, d.DNAME, SUM(e.SAL) AS TOTAL_SAL
    -> FROM EMPLOYEE e
    -> JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
    -> GROUP BY d.DEPTNO, d.DNAME;
+--------+------------+-----------+
| DEPTNO | DNAME      | TOTAL_SAL |
+--------+------------+-----------+
|     10 | RESEARCH   |   1430.00 |
|     20 | ACCOUNTING |  20157.50 |
|     30 | SALES      |   9780.00 |
+--------+------------+-----------+
3 rows in set (0.001 sec)
```

## 10. Display employee number, name and location of the department in which he is working.
```sql
MariaDB [kaushal]> SELECT e.EMPNO, e.ENAME, d.LOCATION
    -> FROM EMPLOYEE E
    -> JOIN DEPARTMENT d ON e.DEPTNO = D.DEPTNO;
+-------+--------+----------+
| EMPNO | ENAME  | LOCATION |
+-------+--------+----------+
|  7369 | SMITH  | DELHI    |
|  7499 | ALLEN  | CHENAI   |
|  7521 | WARD   | CHENAI   |
|  7566 | JONES  | DELHI    |
|  7654 | MARTIN | CHENAI   |
|  7698 | BLAKE  | CHENAI   |
|  7782 | CLARK  | DELHI    |
|  7788 | SCOTT  | DELHI    |
|  7839 | KING   | DELHI    |
|  7844 | TURNER | CHENAI   |
|  7876 | ADAMS  | DELHI    |
|  7900 | JAMES  | CHENAI   |
|  7902 | FORD   | DELHI    |
|  7934 | MILLER | MUMBAI   |
+-------+--------+----------+
14 rows in set (0.001 sec)
```

## 11. Display employee name and department name for each employee.
```sql
MariaDB [kaushal]> SELECT e.ENAME, d.DNAME
    -> FROM EMPLOYEE e
    -> JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO;
+--------+------------+
| ENAME  | DNAME      |
+--------+------------+
| SMITH  | ACCOUNTING |
| ALLEN  | SALES      |
| WARD   | SALES      |
| JONES  | ACCOUNTING |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| CLARK  | ACCOUNTING |
| SCOTT  | ACCOUNTING |
| KING   | ACCOUNTING |
| TURNER | SALES      |
| ADAMS  | ACCOUNTING |
| JAMES  | SALES      |
| FORD   | ACCOUNTING |
| MILLER | RESEARCH   |
+--------+------------+
14 rows in set (0.001 sec)
```


