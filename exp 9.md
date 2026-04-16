
### Experimente 9

## Q1.Display the name of emp name who earns highest salary.
```sql
MariaDB [kaushal]> SELECT Ename
    -> FROM Employee
    -> ORDER BY SAL DESC
    -> LIMIT 1;
+-------+
| Ename |
+-------+
| KING  |
+-------+
1 row in set (0.045 sec)
```

## Q2.Display the employee number and name of employee working as clerk and earning highest salary among clerks.
```sql
MariaDB [kaushal]> SELECT Empno,Ename
    -> FROM Employee
    -> WHERE JOB = 'CLERK'
    -> AND SAL = (SELECT MAX(SAL) FROM Employee WHERE JOB = 'CLERK');
+-------+--------+
| Empno | Ename  |
+-------+--------+
|  7934 | MILLER |
+-------+--------+
1 row in set (0.012 sec)
```

## Q3.Display the names of the salesman who earns a salary more than the highest salary of any clerk'
```sql
MariaDB [kaushal]> SELECT Ename
    -> FROM Employee
    -> WHERE JOB = 'SALESMAN'
    -> AND SAL > (SELECT MAX(SAL) FROM Employee WHERE JOB = 'CLERK');
+--------+
| Ename  |
+--------+
| ALLEN  |
| TURNER |
+--------+
2 rows in set (0.001 sec)
```

## Q4.Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott.
```sql
MariaDB [kaushal]> SELECT Ename
    -> FROM Employee
    -> WHERE JOB = 'CLERK'
    -> AND SAL > (SELECT SAL FROM Employee WHERE Ename = 'JAMES')
    -> AND SAL < (SELECT SAL FROM Employee WHERE Ename = 'SCOTT');
+--------+
| Ename  |
+--------+
| ADAMS  |
| MILLER |
+--------+
2 rows in set (0.001 sec)
```

## Q5.Display the names of employees who earn a sal more than that of james or that of the salary greater than that of scott.
```sql
MariaDB [kaushal]> SELECT Ename
    -> FROM Employee
    -> WHERE SAL > (SELECT SAL FROM Employee WHERE Ename = 'JAMES')
    -> OR SAL > (SELECT SAL FROM Employee WHERE Ename = 'SCOTT');
+--------+
| Ename  |
+--------+
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| BLAKE  |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| FORD   |
| MILLER |
+--------+
12 rows in set (0.001 sec)
```

## Q6.Display the names of employees who earn a highest salary in their respective department.
```sql
MariaDB [kaushal]> SELECT Ename,Deptno,SAL
    -> FROM Employee AS E
    -> WHERE SAL = (SELECT MAX(SAL) FROM Employee WHERE Deptno = E.Deptno);
+--------+--------+---------+
| Ename  | Deptno | SAL     |
+--------+--------+---------+
| BLAKE  |     30 | 3135.00 |
| KING   |     20 | 5500.00 |
| MILLER |     10 | 1430.00 |
+--------+--------+---------+
3 rows in set (0.005 sec)
```

## Q7..Display the names of employees who earn a highest salary in their respective job groups.
```sql
MariaDB [kaushal]> SELECT Ename,JOB,SAL
    -> FROM Employee AS E
    -> WHERE SAL = (SELECT MAX(SAL) FROM Employee WHERE JOB = E.JOB);
+--------+-----------+---------+
| Ename  | JOB       | SAL     |
+--------+-----------+---------+
| ALLEN  | SALESMAN  | 1600.00 |
| JONES  | MANAGER   | 3272.50 |
| SCOTT  | ANALYST   | 3300.00 |
| KING   | PRESIDENT | 5500.00 |
| FORD   | ANALYST   | 3300.00 |
| MILLER | CLERK     | 1430.00 |
+--------+-----------+---------+
6 rows in set (0.001 sec)
```

## Q8.Display the names of employees who working in accounting dept .
```sql
MariaDB [kaushal]> SELECT Ename
    -> FROM Employee
    -> WHERE Deptno = (SELECT Deptno FROM Department WHERE Dname = 'ACCOUNTING');
+-------+
| Ename |
+-------+
| SMITH |
| JONES |
| CLARK |
| SCOTT |
| KING  |
| ADAMS |
| FORD  |
+-------+
7 rows in set (0.003 sec)
```

## Q9.Display the names of employees who are working in chicago.
```sql
MariaDB [kaushal]> SELECT Ename
    -> FROM Employee
    -> WHERE Deptno = (SELECT Deptno FROM Department WHERE LOCATION = "MUMBAI");
+--------+
| Ename  |
+--------+
| MILLER |
+--------+
1 row in set (0.001 sec)
```

## Q10.Display the job group having tatal salary greater than the maximum salary for managers.
```sql
MariaDB [kaushal]> SELECT JOB,SUM(SAL) AS TOTAL_SALARY
    -> FROM Employee
    -> GROUP BY JOB
    -> HAVING SUM(SAL)>(SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = "MANAGER");
+-----------+--------------+
| JOB       | TOTAL_SALARY |
+-----------+--------------+
| ANALYST   |      6600.00 |
| CLERK     |      4565.00 |
| MANAGER   |      9102.50 |
| PRESIDENT |      5500.00 |
| SALESMAN  |      5600.00 |
+-----------+--------------+
5 rows in set (0.001 sec)
```
