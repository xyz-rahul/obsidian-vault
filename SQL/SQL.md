
## SQL quey order of execution
![[Pasted image 20230921140038.png]]

## IF-ELSE operations | Using Conditional Logic in a SELECT Statement

Use the CASE expression

```sql
 select ename,sal,
     case 
		  when sal <= 2000 then 'UNDERPAID'
          when sal >= 4000 then 'OVERPAID'
          else 'OK'
     end as status
from emp
```

```
ENAME            SAL  STATUS
------------------------------
SMITH.           800  UNDERPAID
ALLEN           1600  UNDERPAID
WARD            1250  UNDERPAID
```


## Limiting the Number of Rows Returned
Use the built-in function provided by your database

```MySQL
select *
from emp limit 5
```


## Returning n Random Records from a Table
Use the built-in RAND function in conjunction with LIMIT and ORDER BY:

```Mysql
select ename,job
from emp
order by rand() limit 5
```

## Finding Null Values
To determine whether a value is null, you must use IS NULL:

```MySQL
select *
from emp
where comm is null
```


## Transforming Nulls into Real Values
You have rows that contain nulls and would like to return non-null values in place of those nulls.
1. The first approach uses the `COALESCE` function, which is a standard SQL function supported by many database systems. It returns the first non-null value in the list of its arguments. In this case, it returns the value of "comm" if it is not null and substitutes 0 if "comm" is null.

```sql
select coalesce(comm, 0)
from emp
```

2. The second approach uses a `CASE` expression to achieve the same result. It checks if "comm" is not null and returns its value; otherwise, it returns 0.

```sql
select case
           when comm is not null then comm
           else 0
       end
from emp
```

Both queries will return the same result, replacing null values in the "comm" column with 0. You can choose the one that you find more readable or that aligns better with your database system's conventions.

# Sorting Query Results

### Sorting by Multiple Fields:

You want to sort the rows from the `EMP` table first by `DEPTNO` ascending and then by `sal` descending:

```sql
SELECT empno, deptno, sal, ename, job
FROM emp
ORDER BY deptno ASC, sal DESC;
```

### Sorting by Substrings:

You want to sort the results of a query by specific parts of the `job` column using the `SUBSTR` function:

```sql
SELECT ename, job
FROM emp
ORDER BY substr(job, length(job) - 1);
```

### Dealing with Nulls When Sorting:

You want to sort the results by the `comm` column, placing non-null values first and null values last:

```sql
SELECT ename, sal, comm
FROM (
  SELECT ename, sal, comm,
         CASE WHEN comm IS NULL THEN 0 ELSE 1 END AS is_null
  FROM emp
) x
ORDER BY is_null DESC, comm;
```

## Sorting on a Data-Dependent Key

You want to sort based on some conditional logic.For example, if JOB is SALES‐ MAN, you want to sort on COMM; otherwise, you want to sort by SAL. You want to return the following result set:

Use a CASE expression in the ORDER BY clause:
```SQL
select ename,sal,job,comm
from emp
order by case when job = 'SALESMAN' then comm else sal end
```

## Retrieving Values from One Table That Do Not Exist in Another | MINUS

In MySQL, you can use a subquery to find all `DEPTNO` values from the `EMP` table that do not exist in the `DEPT` table by using a `LEFT JOIN` and checking for `NULL` values in the `DEPT` table's columns in the outer query:

```sql
SELECT e.deptno
FROM emp e
LEFT JOIN dept d ON e.deptno = d.deptno
WHERE d.deptno IS NULL;
```

This query selects all `DEPTNO` values from the `EMP` table (`e`) that do not have a matching `deptno` in the `DEPT` table (`d`), effectively finding the `DEPTNOs` that do not exist in the `DEPT` table.

Note that the `LEFT JOIN` is used to combine rows from both tables based on the `deptno` column, and the `WHERE d.deptno IS NULL` condition filters out rows where no match was found in the `DEPT` table.



## Avoiding Cartesian Products in SQL Queries

**Problem:**
You want to retrieve the names of employees in department 10 along with the location of their respective departments. The following query produces incorrect data:

```sql
SELECT e.ename, d.loc
FROM emp e, dept d
WHERE e.deptno = 10;
```

![[Pasted image 20230921161202.png|]]


**Solution:**
To obtain the correct result set, use a join between the tables in the `FROM` clause:

```sql
SELECT e.ename, d.loc
FROM emp e, dept d
WHERE e.deptno = 10
  AND d.deptno = e.deptno;
```

NOTE:
	You can see that department 10 is in New York, and thus you can know that returning employees with any location other than New York is incorrect. The number of rows returned by the incorrect query is the product of the cardinalities of the two tables in the FROM clause. In the original query, the filter on EMP for department 10 will result in three rows. Because there is no filter for DEPT, all four rows from DEPT are returned. Three multiplied by four is twelve, so the incorrect query returns twelve rows.


# Window Function
https://dev.mysql.com/doc/refman/8.0/en/window-functions-usage.html
A window function performs an aggregate-like operation on a set of query rows. However, whereas an aggregate operation groups query rows into a single result row, a window function produces a result for each query row:

To use a window function we need `over()` clause 
`_over_clause_: {OVER (_window_spec_) | OVER _window_name_}`

`_window_spec_: [_window_name_] [_partition_clause_] [_order_clause_] [_frame_clause_]`




```mysql

mysql> SELECT year, country, product, profit, ROW_NUMBER() OVER(PARTITION BY country) AS row_num1, ROW_NUMBER() OVER(PARTITION BY country ORDER BY year, product) AS row_num2 FROM sales;


+------+---------+------------+--------+----------+----------+
| year | country |   product  | profit | row_num1 | row_num2 |
+------+---------+------------+--------+----------+----------+
| 2000 | Finland |  Computer  |  1500  |    2     |    1     |
| 2000 | Finland |    Phone   |  100   |    1     |    2     |
| 2001 | Finland |    Phone   |   10   |    3     |    3     |
| 2000 |  India  | Calculator |   75   |    2     |    1     |
| 2000 |  India  | Calculator |   75   |    3     |    2     |
| 2000 |  India  |  Computer  |  1200  |    1     |    3     |
| 2000 |   USA   | Calculator |   75   |    5     |    1     |
| 2000 |   USA   |  Computer  |  1500  |    4     |    2     |
| 2001 |   USA   | Calculator |   50   |    2     |    3     |
| 2001 |   USA   |  Computer  |  1500  |    3     |    4     |
| 2001 |   USA   |  Computer  |  1200  |    7     |    5     |
| 2001 |   USA   |     TV     |  150   |    1     |    6     |
| 2001 |   USA   |     TV     |  100   |    6     |    7     |
+------+---------+------------+--------+----------+----------+


```


Useful aggregate function in MySQL
Certainly, here are the common window functions in MySQL with one-line explanations:

**Ranking Functions:**
- ROW_NUMBER() - Assigns a unique number to each row.
- `RANK()`: Assigns the same rank to rows with the same values and leaves gaps in the ranking for tied rows. For example, if two rows have the same highest value, they both get assigned a rank of 1, and the next row gets a rank of 3.
- `DENSE_RANK()`: Assigns the same rank to rows with the same values and does not leave gaps in the ranking for tied rows. For example, if two rows have the same highest value, they both get assigned a rank of 1, and the next row gets a rank of 2.
- ![[Pasted image 20230921210033.png]]

- NTILE(n) - Divides rows into "n" roughly equal parts.
		Divides a partition into _`N`_ groups (buckets), assigns each row in the partition its bucket number, and returns the bucket number of the current row within its partition. For example, if _`N`_ is 4, `NTILE()` divides rows into four buckets. If _`N`_ is 100, `NTILE()` divides rows into 100 buckets.


```mysql

mysql> 
	SELECT 
	val, 
	ROW_NUMBER() OVER w AS 'row_number', 
	NTILE(2) OVER w AS 'ntile2', 
	NTILE(4) OVER w AS 'ntile4' 
	FROM numbers WINDOW w AS (ORDER BY val);

+------+------------+--------+--------+
| val  | row_number | ntile2 | ntile4 |
+------+------------+--------+--------+
| 1    | 1          | 1      | 1      |
| 1    | 2          | 1      | 1      |
| 2    | 3          | 1      | 1      |
| 3    | 4          | 1      | 2      |
| 3    | 5          | 1      | 2      |
| 3    | 6          | 2      | 3      |
| 4    | 7          | 2      | 3      |
| 4    | 8          | 2      | 4      |
| 5    | 9          | 2      | 4      |
+------+------------+--------+--------+

```


**Lead and Lag Functions:**
- LEAD() - Gets the value in the next row.
- LAG() - Gets the value in the previous row.
![[Pasted image 20230921210809.png]]

**Aggregation Functions:**
- SUM() - Calculates the sum of a column.
- AVG() - Calculates the average of a column.
- MAX() - Returns the maximum value in a column.
- MIN() - Returns the minimum value in a column.
- COUNT() - Counts rows or non-null values.

**First and Last Value Functions:**
- FIRST_VALUE() - Retrieves the value from the first row.
- LAST_VALUE() - Retrieves the value from the last row.

**Percentile and Cumulative Distribution Functions:**
- PERCENT_RANK() - Calculates relative rank as a percentage.
![[Pasted image 20230921211010.png]]

