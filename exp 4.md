#  PRACTICAL QUESTION - 4 :-
---
## 1. LIST OF EMPLOYEE JOIN COMPANY BEFORE 30 JUNE 80 0R AFTER 31 DEC 81.
```SQL
MariaDB [kaushal]> select ename from employee
    -> where hiredate< '1980-06-30' and hiredate >'1981-12-31';
Empty set (0.001 sec)
```
---
## 2. display name whose names have second alphabet 'a'.
```sql
MariaDB [kaushal]> select ename from employee
    -> where ename like "_a%";
+--------+
| ename  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.001 sec)
```
---
## 3. exact five digits long name of employee.
```sql
MariaDB [kaushal]> select ename from employee
    -> where ename like "_____";
+-------+
| ename |
+-------+
| SMITH |
| ALLEN |
| JONES |
| BLAKE |
| CLARK |
| SCOTT |
| ADAMS |
| JAMES |
+-------+
8 rows in set (0.001 sec)
```
---
## 4. employee having second alphabet 'e' in name.
```sql
MariaDB [kaushal]> select ename from employee
    -> where ename like "_e%";
Empty set (0.001 sec)
```
---
## 5. employees not working aas salesman, clerk,analyst.
```sql
MariaDB [kaushal]> select ename from employee
    -> where job not in ('clerk','analyst','salesman');
+-------+
| ename |
+-------+
| JONES |
| BLAKE |
| CLARK |
| KING  |
+-------+
4 rows in set (0.002 sec)
```
---
## 6. name of employee with their annual sal.the name of highest sal should appera first.
```sql
MariaDB [kaushal]> select ename,(sal*12) as annual_salary from employee
    -> order by sal desc;
+--------+---------------+
| ename  | annual_salary |
+--------+---------------+
| KING   |         60000 |
| SCOTT  |         36000 |
| FORD   |         36000 |
| JONES  |         35700 |
| BLAKE  |         34200 |
| CLARK  |         29400 |
| ALLEN  |         19200 |
| TURNER |         18000 |
| MILLER |         15600 |
| MARTIN |         15000 |
| WARD   |         15000 |
| ADAMS  |         13200 |
| JAMES  |         11400 |
| SMITH  |          9600 |
+--------+---------------+
14 rows in set (0.001 sec)
```
---
## 7. name,hra,pf,da,sal for each employee where output should be in order of total salary,hra(15% of sal),da(10% of sal),pf(5% of sal),total sal(sal+hra+df)-pf.
```sql
MariaDB [kaushal]> select sal,(sal*0.15) as hra,
    -> (sal*0.10) as da,
    -> (sal*0.05) as pf
    -> from employee
    -> order by (sal+hra+da)-pf;
+------+--------+--------+--------+
| sal  | hra    | da     | pf     |
+------+--------+--------+--------+
|  800 | 120.00 |  80.00 |  40.00 |
|  950 | 142.50 |  95.00 |  47.50 |
| 1100 | 165.00 | 110.00 |  55.00 |
| 1250 | 187.50 | 125.00 |  62.50 |
| 1250 | 187.50 | 125.00 |  62.50 |
| 1300 | 195.00 | 130.00 |  65.00 |
| 1500 | 225.00 | 150.00 |  75.00 |
| 1600 | 240.00 | 160.00 |  80.00 |
| 2450 | 367.50 | 245.00 | 122.50 |
| 2850 | 427.50 | 285.00 | 142.50 |
| 2975 | 446.25 | 297.50 | 148.75 |
| 3000 | 450.00 | 300.00 | 150.00 |
| 3000 | 450.00 | 300.00 | 150.00 |
| 5000 | 750.00 | 500.00 | 250.00 |
+------+--------+--------+--------+
14 rows in set (0.002 sec)
```
---
## 8. update sal for employees with 10% increment who are not elligible for commission.
```sql
MariaDB [kaushal]> select ename,job,sal,(0.10*sal+sal) as updated_salary
    -> from employee
    -> where comm is null ;
+--------+-----------+------+----------------+
| ename  | job       | sal  | updated_salary |
+--------+-----------+------+----------------+
| SMITH  | CLERK     |  800 |         880.00 |
| JONES  | MANAGER   | 2975 |        3272.50 |
| BLAKE  | MANAGER   | 2850 |        3135.00 |
| CLARK  | MANAGER   | 2450 |        2695.00 |
| SCOTT  | ANALYST   | 3000 |        3300.00 |
| KING   | PRESIDENT | 5000 |        5500.00 |
| ADAMS  | CLERK     | 1100 |        1210.00 |
| JAMES  | CLERK     |  950 |        1045.00 |
| FORD   | ANALYST   | 3000 |        3300.00 |
| MILLER | CLERK     | 1300 |        1430.00 |
+--------+-----------+------+----------------+
10 rows in set (0.001 sec)
```
---
## 9. display employee whose sal is more than 3000 after giving 20% increment.
```sql

MariaDB [kaushal]> select ename,(0.20*sal+sal) as updated_salary
    -> from employee
    -> where sal>3000;
+-------+----------------+
| ename | updated_salary |
+-------+----------------+
| KING  |        6000.00 |
+-------+----------------+
1 row in set (0.001 sec)
```
---
## 10.  employee having sal digit 3 atleast.
```sql
MariaDB [kaushal]> select ename,sal
    -> from employee
    -> where sal like '___';
+-------+------+
| ename | sal  |
+-------+------+
| SMITH |  800 |
| JAMES |  950 |
+-------+------+
2 rows in set (0.001 sec)
```
----