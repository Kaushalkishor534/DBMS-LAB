# PRACTICAL QUESTION - 5 :-
---
## 1. DISPLAY TOTAL NO. OF EMPLOYEE IN THE COMPANY.
```SQL
MariaDB [kaushal]> SELECT COUNT(*) ENAME FROM EMPLOYEE;
+-------+
| ENAME |
+-------+
|    14 |
+-------+
1 row in set (0.050 sec)
```
##  2. DISPLAY TOTAL SALARY PAID TO EMPLOYEES.
```SQL
MariaDB [kaushal]> SELECT SUM(SAL) AS TOTAL_SALARY FROM EMPLOYEE;
+--------------+
| TOTAL_SALARY |
+--------------+
|        29025 |
+--------------+
1 row in set (0.001 sec)
```
## 3. DISPLAY MAX SALARY FROM EMPLOYEE.
```SQL
MariaDB [kaushal]> SELECT MAX(SAL) AS MAX_SALARY FROM EMPLOYEE;
+------------+
| MAX_SALARY |
+------------+
|       5000 |
+------------+
1 row in set (0.001 sec)
```
## 4. DISPLAY MIN SALARY FROM EMPLOYEE.
```SQL
MariaDB [kaushal]> SELECT MIN(SAL) AS MIN_SALARY FROM EMPLOYEE;
+------------+
| MIN_SALARY |
+------------+
|        800 |
+------------+
1 row in set (0.001 sec)
```
## 5. DISPLAY AVERAGE SALARY FROM EMPLOYEE.
```SQL
MariaDB [kaushal]> SELECT AVG(SAL) AS AVG_SALARY FROM EMPLOYEE;
+------------+
| AVG_SALARY |
+------------+
|  2073.2143 |
+------------+
1 row in set (0.001 sec)
```
### ROUND VALUE
```SQL
MariaDB [kaushal]> SELECT ROUND(AVG(SAL),1) AS AVG_SALARY FROM EMPLOYEE;
+------------+
| AVG_SALARY |
+------------+
|     2073.2 |
+------------+
1 row in set (0.001 sec)
```
## 6. DISPLAY MAX SAL PAID TO CLERK.
```SQL
MariaDB [kaushal]> SELECT MAX(SAL) AS MAX_SALARY FROM EMPLOYEE
    -> WHERE JOB = 'CLERK';
+------------+
| MAX_SALARY |
+------------+
|       1300 |
+------------+
1 row in set (0.001 sec)
```
## 7. DISPLAY MAX SAL PAID IN DEPT 20.
```SQL
MariaDB [kaushal]> SELECT MAX(SAL) AS MAX_SALARY FROM EMPLOYEE
    -> WHERE DEPTNO=20;
+------------+
| MAX_SALARY |
+------------+
|       5000 |
+------------+
1 row in set (0.001 sec)
```
## 8. DISPLAY MIN SAL PAID TO ANY SALESMAN.
```SQL
MariaDB [kaushal]> SELECT MIN(SAL)  AS MIN_SAL FROM EMPLOYEE
    -> WHERE JOB ='SALESMAN';
+---------+
| MIN_SAL |
+---------+
|    1250 |
+---------+
1 row in set (0.001 sec)
```
## 9. DISPLAY AVERAGE SAL BY MANAGERS.
```SQL
MariaDB [kaushal]> SELECT AVG(SAL) AS AVG_SALARY FROM EMPLOYEE
    -> WHERE JOB ='MANAGER';
+------------+
| AVG_SALARY |
+------------+
|  2758.3333 |
+------------+
1 row in set (0.001 sec)
```
## 10. TOTAL SALARY  DRAWN BY ANALYST WORKING IN DEPT 40.
```SQL
MariaDB [kaushal]> SELECT SUM(SAL) AS SUM_SAL FROM EMPLOYEE
    -> WHERE DEPTNO=40 AND JOB='ANALYST';
+---------+
| SUM_SAL |
+---------+
|    3000 |
+---------+
1 row in set (0.001 sec)
```
## 11. DISPLAY NAMES OF EMPLOYEE IN UPPER CASE.
```SQL
MariaDB [kaushal]> SELECT UPPER(ENAME) FROM EMPLOYEE;
+--------------+
| UPPER(ENAME) |
+--------------+
| SMITH        |
| ALLEN        |
| WARD         |
| JONES        |
| MARTIN       |
| BLAKE        |
| CLARK        |
| SCOTT        |
| KING         |
| TURNER       |
| ADAMS        |
| JAMES        |
| FORD         |
| MILLER       |
+--------------+
14 rows in set (0.001 sec)
```
## 12. DISPLAY NAMES OF EMPLOYEE IN LOWER CASE.
```SQL
MariaDB [kaushal]> SELECT LOWER(ENAME) FROM EMPLOYEE;
+--------------+
| LOWER(ENAME) |
+--------------+
| smith        |
| allen        |
| ward         |
| jones        |
| martin       |
| blake        |
| clark        |
| scott        |
| king         |
| turner       |
| adams        |
| james        |
| ford         |
| miller       |
+--------------+
14 rows in set (0.001 sec)
```
## 13. DISPLAY NAMES OF EMPLOYEE IN PROPER CASE.
```SQL
MariaDB [kaushal]> SELECT CONCAT(UPPER(SUBSTR(ENAME,1,1)),LOWER(SUBSTR(ENAME,2))) FROM EMPLOYEE;
+---------------------------------------------------------+
| CONCAT(UPPER(SUBSTR(ENAME,1,1)),LOWER(SUBSTR(ENAME,2))) |
+---------------------------------------------------------+
| Smith                                                   |
| Allen                                                   |
| Ward                                                    |
| Jones                                                   |
| Martin                                                  |
| Blake                                                   |
| Clark                                                   |
| Scott                                                   |
| King                                                    |
| Turner                                                  |
| Adams                                                   |
| James                                                   |
| Ford                                                    |
| Miller                                                  |
+---------------------------------------------------------+
14 rows in set (0.001 sec)
```
## 14. DISPLAY LENGTH OF YOUR NAME.
```SQL
MariaDB [kaushal]> SELECT LENGTH('KAUSHAL');
+-------------------+
| LENGTH('KAUSHAL') |
+-------------------+
|                 7 |
+-------------------+
1 row in set (0.001 sec)

```
## 15. DISPLAY LENGTH OF NAMES FROM EMPLOYEE.
```SQL
MariaDB [kaushal]> SELECT LENGTH(ENAME) FROM EMPLOYEE;
+---------------+
| LENGTH(ENAME) |
+---------------+
|             5 |
|             5 |
|             4 |
|             5 |
|             6 |
|             5 |
|             5 |
|             5 |
|             4 |
|             6 |
|             5 |
|             5 |
|             4 |
|             6 |
+---------------+
14 rows in set (0.001 sec)
```
---
---