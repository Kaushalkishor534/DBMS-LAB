
# Experiment 11

## Q1.Delete those employees who joined the company before 31 dec-82 while there dept location is ‘Mumbai' or 'Delhi'.
```sql
MariaDB [kaushal]> DELETE FROM EMPLOYEE
    -> WHERE HIREDATE < '1982-12-31'
    -> AND DEPTNO IN (
    -> SELECT DEPTNO
    -> FROM DEPARTMENT
    -> WHERE LOCATION IN ('Mumbai', 'Delhi')
    -> );
Query OK, 0 rows affected (0.001 sec)
```

## Q2.Display employee name, job, deptname, location for all who are working as managers.
```SQL
MariaDB [kaushal]> SELECT E.ENAME,E.JOB,D.DNAME,D.LOCATION
    -> FROM EMPLOYEE E
    -> JOIN DEPARTMENT D
    -> ON E.DEPTNO = D.DEPTNO
    -> WHERE E.JOB = 'MANAGER';
+-------+---------+-------+----------+
| ENAME | JOB     | DNAME | LOCATION |
+-------+---------+-------+----------+
| BLAKE | MANAGER | SALES | CHENAI   |
+-------+---------+-------+----------+
1 row in set (0.012 sec)
```

## Q3.Display name and salary of ford if his sal is equal to high sal of his grade.
```SQL
MariaDB [kaushal]> SELECT E.ENAME, E.SAL
    -> FROM EMPLOYEE E
    -> JOIN SALGRADE S
    -> ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE E.ENAME = 'FORD'
    -> AND E.SAL = (
    ->     SELECT MAX(E2.SAL)
    ->     FROM EMPLOYEE E2
    ->     JOIN SALGRADE S2
    ->     ON E2.SAL BETWEEN S2.LOSAL AND S2.HISAL
    ->     WHERE S2.GRADE = S.GRADE
    -> );
Empty set (0.008 sec)
```

## Q4.Find out the top 5 earner of company.
```SQL
MariaDB [kaushal]> SELECT ENAME, SAL
    -> FROM EMPLOYEE
    -> ORDER BY SAL DESC
    -> LIMIT 5;
+--------+---------+
| ENAME  | SAL     |
+--------+---------+
| BLAKE  | 3135.00 |
| ALLEN  | 1600.00 |
| TURNER | 1500.00 |
| WARD   | 1250.00 |
| MARTIN | 1250.00 |
+--------+---------+
5 rows in set (0.007 sec)
```

## Q5.Display the name of those employees who are getting highest salary.
```SQL
MariaDB [kaushal]> SELECT ENAME
    -> FROM EMPLOYEE
    -> WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
+-------+
| ENAME |
+-------+
| BLAKE |
+-------+
1 row in set (0.001 sec)
```

## Q6.Display those employees whose salary is equal to average of maximum and minimum.
```SQL
MariaDB [kaushal]> SELECT ENAME, SAL
    -> FROM EMPLOYEE
    -> WHERE SAL = (
    ->     (SELECT MAX(SAL) FROM EMPLOYEE) +
    ->     (SELECT MIN(SAL) FROM EMPLOYEE)
    -> ) / 2;
Empty set (0.002 sec)
```

## Q7.Display dname where at least 3 are working and display only dname
```SQL
MariaDB [kaushal]> SELECT D.DNAME
    -> FROM DEPARTMENT D
    -> JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
    -> GROUP BY D.DNAME
    -> HAVING COUNT(*) >= 3;
+-------+
| DNAME |
+-------+
| SALES |
+-------+
1 row in set (0.002 sec)
```

## Q8. Display name of those managers names whose salary is more than average salary of company.
```SQL
MariaDB [kaushal]> SELECT ENAME
    -> FROM EMPLOYEE
    -> WHERE JOB = 'MANAGER'
    -> AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
+-------+
| ENAME |
+-------+
| BLAKE |
+-------+
1 row in set (0.001 sec)
```

## Q9. Display those managers name whose salary is more than an average salary of his employees.
```SQL
MariaDB [kaushal]> SELECT M.ENAME
    -> FROM EMPLOYEE M
    -> WHERE M.JOB = 'MANAGER'
    -> AND M.SAL > (
    ->     SELECT AVG(E.SAL)
    ->     FROM EMPLOYEE E
    ->     WHERE E.MGR = M.EMPNO
    -> );
+-------+
| ENAME |
+-------+
| BLAKE |
+-------+
1 row in set (0.001 sec)
```

## Q10.Display employee name, sal, comm and net pay for those employees whose net pay are greater than or equal to any other employee salary of the company?
```SQL
MariaDB [kaushal]> SELECT ENAME, SAL, COMM,
    ->        (SAL + IFNULL(COMM,0)) AS NET_PAY
    -> FROM EMPLOYEE
    -> WHERE (SAL + IFNULL(COMM,0)) >= ANY (
    ->     SELECT SAL FROM EMPLOYEE
    -> );
+--------+---------+---------+---------+
| ENAME  | SAL     | COMM    | NET_PAY |
+--------+---------+---------+---------+
| ALLEN  | 1600.00 |  300.00 | 1900.00 |
| WARD   | 1250.00 |  300.00 | 1550.00 |
| MARTIN | 1250.00 | 1400.00 | 2650.00 |
| BLAKE  | 3135.00 |    NULL | 3135.00 |
| TURNER | 1500.00 |    0.00 | 1500.00 |
| ADAMS  | 1210.00 |    NULL | 1210.00 |
| JAMES  | 1045.00 |    NULL | 1045.00 |
+--------+---------+---------+---------+
7 rows in set (0.008 sec)
```
