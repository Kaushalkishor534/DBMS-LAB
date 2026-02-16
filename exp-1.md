## Question 1:
---
### creation of database
```sql
MariaDB [(none)]> CREATE DATABASE emp;
Query OK, 1 row affected (0.003 sec)
MariaDB [(none)]> USE emp;
Database changed
```
### creation of department table
```sql
MariaDB [emp]> CREATE TABLE DEPARTMENT(
    -> DEPT_NO INT(4) PRIMARY KEY,
    -> Dname VARCHAR(15) NOT NULL
    -> );
Query OK, 0 rows affected (0.017 sec)
```
### creation of employee table
```sql
MariaDB [emp]> CREATE TABLE EMPLOYEE (
    -> Empno INT PRIMARY KEY,
    -> Ename VARCHAR(20) NOT NULL,
    -> job VARCHAR(20),
    ->  Mgr INT(4),
    -> Hiredate Date,
    -> Sal INT(10),
    -> Comm INT,
    -> Deptno INT,
    -> FOREIGN KEY (Deptno) REFERENCES DEPARTMENT(DEPT_NO)
    -> );
Query OK, 0 rows affected (0.053 sec)
```
### filling values in department table
```sql
MariaDB [emp]> INSERT INTO DEPARTMENT VALUES (10, 'RESEARCH'),(20, 'ACCOUNTING'),(30, 'SALES'), (40, 'OPERATIONS');
Query OK, 1 row affected (0.002 sec)
```
### filling values in employee table
```sql
MariaDB [emp]> INSERT INTO EMPLOYEE VALUES (7369,'SMITH','CLERK',7902,DATE '1980-12-17',800,NULL,20),(7499,'ALLEN','SALESMAN',7698,DATE '1981-02-20',1600,300,30),(7521,'WARD','SALESMAN',7698,DATE '1981-02-22',1250,300,30),(7566,'JONES','MANAGER',7839,DATE '1981-04-02',2975,NULL,20),(7654,'MARTIN','SALESMAN',7698,DATE '1981-09-28',1250,1400,30),(7698,'BLAKE','MANAGER',7839,DATE '1981-05-01',2850,NULL,30),(7782,'CLARK','MANAGER',7839,DATE '1981-06-09',2450,NULL,20),(7788,'SCOTT','ANALYST',7566,DATE '1982-12-09',3000,NULL,40),(7839,'KING','PRESIDENT',NULL,DATE '1981-11-17',5000,NULL,20),(7844,'TURNER','SALESMAN',7698,DATE '1981-09-08',1500,0,30),(7876,'ADAMS','CLERK',7788,DATE '1983-01-12',1100,NULL,20),(7900,'JAMES','CLERK',7698,DATE '1981-12-03',950,NULL,30), (7902,'FORD','ANALYST',7566,DATE '1981-12-03',3000,NULL,20),(7934,'MILLER','CLERK',7782,DATE '1982-01-23',1300,NULL,10);
Query OK, 1 row affected (0.002 sec)
```
### Create EMPLOYEE_MASTER table with data using EMPLOYEE table
```sql
MariaDB [emp]> CREATE TABLE EMPLOYEE_MASTER AS
    -> SELECT * FROM EMPLOYEE;
Query OK, 14 rows affected (0.040 sec)
Records: 14  Duplicates: 0  Warnings: 0
```
### Delete all records from EMPLOYEE_MASTER whose DEPTNO = 10
```sql
MariaDB [emp]> DELETE FROM EMPLOYEE_MASTER
    -> WHERE DEPTNO = 10;
Query OK, 1 row affected (0.019 sec)
```
### Alter SAL column size to 10,2
```sql
MariaDB [emp]> UPDATE EMPLOYEE_MASTER
    -> SET SAL = SAL + (SAL * 0.10)
    -> WHERE DEPTNO = 20;
Query OK, 6 rows affected (0.020 sec)
Rows matched: 6  Changed: 6  Warnings: 0
```

