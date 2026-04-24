
# Experiment 12

## Q1. Display those employees whose salary is less than his manager but more than salary of any other managers.
```SQL
MariaDB [kaushal]> SELECT E.ENAME
    -> FROM EMPLOYEE E
    -> JOIN EMPLOYEE M ON E.MGR = M.EMPNO
    -> WHERE E.SAL < M.SAL
    -> AND E.SAL > ANY (SELECT SAL FROM EMPLOYEE);
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| TURNER |
+--------+
4 rows in set (0.001 sec)
```

## Q2. Find out the number of employees whose salary is greater than their manager salary?
```SQL
MariaDB [kaushal]> SELECT COUNT(*) AS TOTAL
    -> FROM EMPLOYEE E
    -> JOIN EMPLOYEE M ON E.MGR = M.EMPNO
    -> WHERE E.SAL > M.SAL;
+-------+
| TOTAL |
+-------+
|     0 |
+-------+
1 row in set (0.001 sec)
```

## Q3. Display those managers who are not working under president but they are working under any other manager?
```SQL
MariaDB [kaushal]> SELECT E.ENAME
    -> FROM EMPLOYEE E
    -> JOIN EMPLOYEE M ON E.MGR = M.EMPNO
    -> WHERE E.JOB = 'MANAGER'
    -> AND M.JOB <> 'PRESIDENT';
Empty set (0.001 sec)
```

## Q4. Delete those department where no employee working?
```SQL
MariaDB [kaushal]> DELETE FROM DEPARTMENT
    -> WHERE DEPTNO NOT IN (
    ->     SELECT DISTINCT DEPTNO FROM EMPLOYEE
    -> );
Query OK, 0 rows affected (0.001 sec)
```

## Q5. Delete those records from emp table whose deptno not available in dept table?
```SQL
MariaDB [kaushal]> DELETE FROM EMPLOYEE
    -> WHERE DEPTNO NOT IN (
    ->     SELECT DEPTNO FROM DEPARTMENT
    -> );
Query OK, 0 rows affected (0.001 sec)
```

## Q6. Display those earners whose salary is out of the grade available in sal grade table?
```SQL
MariaDB [kaushal]> SELECT ENAME, SAL
    -> FROM EMPLOYEE
    -> WHERE SAL NOT BETWEEN
    ->     (SELECT MIN(LOSAL) FROM SALGRADE)
    -> AND
    ->     (SELECT MAX(HISAL) FROM SALGRADE);
Empty set (0.044 sec)
```

## Q7. Display employee name, sal, comm. And whose net pay is greater than any other in the company?
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
7 rows in set (0.004 sec)
```

## Q8. Display those employees who are working in sales or research?
```SQL
MariaDB [kaushal]> SELECT E.ENAME
    -> FROM EMPLOYEE E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> WHERE D.DNAME IN ('SALES', 'RESEARCH');
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+
6 rows in set (0.041 sec)
```

## Q9. Display the grade of jones?
```SQL
MariaDB [kaushal]> SELECT S.GRADE
    -> FROM EMPLOYEE E
    -> JOIN SALGRADE S
    -> ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE E.ENAME = 'JONES';
Empty set (0.001 sec)
```

## Q10. Display the department name the no of characters of which is equal to no of employees in any other department?
```SQL
MariaDB [kaushal]> SELECT D.DNAME
    -> FROM DEPARTMENT D
    -> WHERE LENGTH(D.DNAME) IN (
    ->     SELECT COUNT(*)
    ->     FROM EMPLOYEE
    ->     GROUP BY DEPTNO
    -> );
Empty set (0.042 sec)
```
