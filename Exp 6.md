# PRACTTICAL QUESTION - 6:-
---
## 1. DISPLAY EMPNO,ENAME,DEPTNO FROM EMPLOYEE.INSTEAD OF DISPLAY DEPTNO DISPLAY RELATED DEPARTMENT NAME(USE CASE FUNCTION).
```SQL
MariaDB [kaushal]> select empno,ename,
    -> case deptno
    -> when 10 then'research'
    -> when 20 then'accounting'
    -> when 30 then'sales'
    -> when 40 then'operations'
    -> end as department_name
    -> from employee;
+-------+--------+-----------------+
| empno | ename  | department_name |
+-------+--------+-----------------+
|  7369 | SMITH  | accounting      |
|  7499 | ALLEN  | sales           |
|  7521 | WARD   | sales           |
|  7566 | JONES  | accounting      |
|  7654 | MARTIN | sales           |
|  7698 | BLAKE  | sales           |
|  7782 | CLARK  | accounting      |
|  7788 | SCOTT  | operations      |
|  7839 | KING   | accounting      |
|  7844 | TURNER | sales           |
|  7876 | ADAMS  | accounting      |
|  7900 | JAMES  | sales           |
|  7902 | FORD   | accounting      |
|  7934 | MILLER | research        |
+-------+--------+-----------------+
14 rows in set (0.001 sec)
```
---
## 2. display age in days.
```sql
MariaDB [kaushal]> select timestampdiff(day,'2006-02-10',curdate());
+-------------------------------------------+
| timestampdiff(day,'2006-02-10',curdate()) |
+-------------------------------------------+
|                                      7312 |
+-------------------------------------------+
1 row in set (0.001 sec)
```
---
## 3. age in months.
```sql
MariaDB [kaushal]> select timestampdiff(month,'2006-02-10',curdate());
+---------------------------------------------+
| timestampdiff(month,'2006-02-10',curdate()) |
+---------------------------------------------+
|                                         240 |
+---------------------------------------------+
1 row in set (0.001 sec)
```
---
## 4. display current date as 15 august friday 1997.
```sql
MariaDB [kaushal]> select date_format(curdate(),'%d %m %w %y') as curent_date;
+-------------+
| curent_date |
+-------------+
| 17 02 2 26  |
+-------------+
1 row in set (0.001 sec)
```
---
## 5.display following output for  every row.
## 6.SCOTT has joined the company on wednesday 09 12 1982.
```sql
select concat(ename ,'  has joined the company on  ',
    -> dayname(hiredate)  ,'  ',date_format( hiredate,'%d %m %y'))
    -> as emp
    -> from employee;
+-------------------------------------------------------+
| emp                                                   |
+-------------------------------------------------------+
| SMITH  has joined the company on  Wednesday  17 12 80 |
| ALLEN  has joined the company on  Friday  20 02 81    |
| WARD  has joined the company on  Sunday  22 02 81     |
| JONES  has joined the company on  Thursday  02 04 81  |
| MARTIN  has joined the company on  Monday  28 09 81   |
| BLAKE  has joined the company on  Friday  01 05 81    |
| CLARK  has joined the company on  Tuesday  09 06 81   |
| SCOTT  has joined the company on  Thursday  09 12 82  |
| KING  has joined the company on  Tuesday  17 11 81    |
| TURNER  has joined the company on  Tuesday  08 09 81  |
| ADAMS  has joined the company on  Wednesday  12 01 83 |
| JAMES  has joined the company on  Thursday  03 12 81  |
| FORD  has joined the company on  Thursday  03 12 81   |
| MILLER  has joined the company on  Saturday  23 01 82 |
+-------------------------------------------------------+
14 rows in set (0.001 sec)
```
---
## 7. nearest day from current day  for saturday. 
```sql
MariaDB [kaushal]> select date_add(curdate(),interval 3 day);
+------------------------------------+
| date_add(curdate(),interval 3 day) |
+------------------------------------+
| 2026-02-21                         |
+------------------------------------+
1 row in set (0.001 sec)
```
---
## 8. display current time.
```sql
MariaDB [kaushal]> select curtime();
+-----------+
| curtime() |
+-----------+
| 07:54:08  |
+-----------+
1 row in set (0.001 sec)
```

---
## 9. display date of 3 month before the current date.
```sql
MariaDB [kaushal]> select date_sub(curdate(),interval 3 month);
+--------------------------------------+
| date_sub(curdate(),interval 3 month) |
+--------------------------------------+
| 2025-11-18                           |
+--------------------------------------+
1 row in set (0.001 sec)
```

---
## 10. display employee joined company in december.
```sql
MariaDB [kaushal]> select ename,hiredate
    -> from employee
    -> where month(hiredate)=12;
+-------+------------+
| ename | hiredate   |
+-------+------------+
| SMITH | 1980-12-17 |
| SCOTT | 1982-12-09 |
| JAMES | 1981-12-03 |
| FORD  | 1981-12-03 |
+-------+------------+
4 rows in set (0.001 sec)
```
---
## 11.

## 12. show names of employee who have 10% of salary equal to date of hire.
```sql
MariaDB [kaushal]> select ename,(sal*0.10)as salary,year(hiredate)
    -> from employee
    -> where (sal*0.10) = year(hiredate);
Empty set (0.001 sec)
```
---
## 13. show the names of employee joined before 15 of their months.
```sql
MariaDB [kaushal]> select ename, hiredate from employee
    -> where date_format(hiredate,'%d') < 15;
+--------+------------+
| ename  | hiredate   |
+--------+------------+
| JONES  | 1981-04-02 |
| BLAKE  | 1981-05-01 |
| CLARK  | 1981-06-09 |
| SCOTT  | 1982-12-09 |
| TURNER | 1981-09-08 |
| ADAMS  | 1983-01-12 |
| JAMES  | 1981-12-03 |
| FORD   | 1981-12-03 |
+--------+------------+
8 rows in set (0.001 sec)
```
---
## 14. show the names of employee joined before 15 of their months.
```sql
MariaDB [kaushal]> select ename, hiredate from employee
    -> where date_format(hiredate,'%d') < 15;
+--------+------------+
| ename  | hiredate   |
+--------+------------+
| JONES  | 1981-04-02 |
| BLAKE  | 1981-05-01 |
| CLARK  | 1981-06-09 |
| SCOTT  | 1982-12-09 |
| TURNER | 1981-09-08 |
| ADAMS  | 1983-01-12 |
| JAMES  | 1981-12-03 |
| FORD   | 1981-12-03 |
+--------+------------+
8 rows in set (0.001 sec)
```
---
## 15. show names of employee having date of join equal to their deptno.
```sql
MariaDB [kaushal]> select ename,hiredate,deptno
    -> from employee
    -> where date_format(hiredate,'%d') = deptno;
Empty set (0.001 sec)
```
----
---