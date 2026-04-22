
# Experiment 10

## Q1. Display the names of employees from department number 10 with salary greater than that of any employee working in other departments.
```sql
MariaDB [kaushal]> SELECT ENAME
    -> FROM Employee
    -> WHERE Deptno = 10
    -> AND SAL > ANY (SELECT SAL FROM Employee WHERE Deptno <> 10);
+--------+
| ENAME  |
+--------+
| MILLER |
+--------+
1 row in set (0.076 sec)
```

## Q2.Display the names of employees from department number 10 with salary greater than that of all employee working in other departments.
```sql
MariaDB [kaushal]> SELECT ENAME
    -> FROM Employee
    -> WHERE Deptno = 10
    -> AND SAL > ALL(SELECT SAL FROM Employee WHERE Deptno <> 10);
Empty set (0.001 sec)
```

## Q3.Display the details of employees who are in sales dept and where grade is c.
```sql
MariaDB [kaushal]> SELECT *
    -> FROM Employee e
    -> JOIN Department d ON e.Deptno = d.Deptno
    -> JOIN SALGRADE S ON e.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE d.Dname = "SALES"
    -> AND S.GRADE = "C";
+-------+--------+----------+------+------------+---------+--------+--------+--------+-------+----------+-------+-------+-------+
| Empno | Ename  | Job      | Mgr  | Hiredate   | Sal     | Comm   | Deptno| Deptno | Dname | LOCATION | GRADE | LOSAL | HISAL |
+-------+--------+----------+------+------------+---------+--------+--------+--------+-------+----------+-------+-------+-------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600.00 | 300.00 |     30|     30 | SALES | CHENAI   | C     |  1401 |  2000 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 |   0.00 |     30|     30 | SALES | CHENAI   | C     |  1401 |  2000 |
+-------+--------+----------+------+------------+---------+--------+--------+--------+-------+----------+-------+-------+-------+
2 rows in set (0.019 sec)
```

## Q4.Display those who are not managers and who manages anyone.
```sql
MariaDB [kaushal]> SELECT Ename
    -> FROM Employee
    -> WHERE JOB <> "MANAGER"
    -> AND Empno IN(SELECT MGR FROM Employee WHERE MGR IS NOT NULL);
+-------+
| Ename |
+-------+
| SCOTT |
| KING  |
| FORD  |
+-------+
3 rows in set (0.004 sec)
```

## Q5.Display those employees whose manager name is jones.
```sql
MariaDB [kaushal]> SELECT e.Ename
    -> FROM Employee e
    -> JOIN Employee M ON e.MGR = M.Empno
    -> WHERE M.Ename = 'JONES';
+-------+
| Ename |
+-------+
| SCOTT |
| FORD  |
+-------+
2 rows in set (0.001 sec)
```

## Q6.Display ename who are working in sales dept.
```sql
MariaDB [kaushal]> SELECT e.Ename
    -> FROM Employee e
    -> JOIN Department D
    -> ON e.Deptno = D.Deptno
    -> WHERE D.Dname = "SALES";
+--------+
| Ename  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+
6 rows in set (0.001 sec)
```

## Q7.Display employee name,deptname,salary and comm. For those sal in between 2000 to 5000 while location is chennai.
```sql
MariaDB [kaushal]> SELECT e.Ename,d.Dname,e.SAL,e.COMM
    -> FROM Employee e
    -> JOIN Department d
    -> ON e.Deptno = d.Deptno
    -> WHERE e.SAL BETWEEN 2000 AND 5000
    -> AND D.LOCATION = "Chennai";
Empty set (0.001 sec)
```

## Q8.Display those employees whose salary greater than his manager salary.
```sql
MariaDB [kaushal]> SELECT e.Ename
    -> FROM Employee e
    -> JOIN Employee M
    -> ON e.MGR = M.Empno
    -> WHERE e.SAL > M.SAL;
+-------+
| Ename |
+-------+
| SCOTT |
| FORD  |
+-------+
2 rows in set (0.001 sec)
```

## Q9.Display those employees who are working in the same dept where his manager is working.
```sql
MariaDB [kaushal]> SELECT e.Ename
    -> FROM Employee e
    -> JOIN Employee M
    -> ON e.MGR = M.Empno
    -> WHERE e.Deptno = M.Deptno;
+--------+
| Ename  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| CLARK  |
| SCOTT  |
| TURNER |
| ADAMS  |
| JAMES  |
| FORD   |
+--------+
11 rows in set (0.001 sec)
```

## Q10. Display grade and employees name for the dept no 10 or 30 but grade is not D, while joined the company before 31-Dec-82.
```sql
MariaDB [kaushal]> SELECT e.Ename,S.GRADE
    -> FROM Employee e
    -> JOIN SALGRADE S
    -> ON e.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE e.Deptno IN (10,30)
    -> AND S.GRADE <> "D"
    -> AND e.HIREDATE < "1982-12-31";
+--------+-------+
| Ename  | GRADE |
+--------+-------+
| ALLEN  | C     |
| WARD   | B     |
| MARTIN | B     |
| BLAKE  | E     |
| TURNER | C     |
| JAMES  | A     |
| MILLER | C     |
+--------+-------+
7 rows in set (0.001 sec)
```
