### Creating and managing databases![Copy Icon](https://www.cockroachlabs.com/images/icons/copy-icon.svg)

#### [CREATE DATABASE](https://www.cockroachlabs.com/docs/stable/create-database)

Creates a new database.

```sql
CREATE DATABASE bank;
```

#### [DROP DATABASE](https://www.cockroachlabs.com/docs/stable/drop-database)

Delete a database and all of its contents.

```sql
DROP DATABASE bank;
```

#### [SHOW DATABASES](https://www.cockroachlabs.com/docs/stable/show-databases)*

Show all databases in your cluster.

```sql
SHOW DATABASES;
```

### ALIASES

#### COLUMNS

```sql
SELECT name AS city_name
FROM city;
```

#### TABLES

```sql
SELECT co.name, ci.name
FROM city AS ci
JOIN country AS co
  ON ci.country_id = co.id;
```

### FILTERING THE OUTPUT

#### COMPARISON OPERATORS

Fetch names of cities that have a rating above 3:

```sql
SELECT name
FROM city
WHERE rating > 3;
```

Fetch names of cities that are neither Berlin nor Madrid:

```sql
SELECT name
FROM city
WHERE name != 'Berlin'
  AND name != 'Madrid';
```

#### TEXT OPERATORS

Fetch names of cities that start with a 'P' or end with an 's':

```sql
SELECT name
FROM city
WHERE name LIKE 'P%'
  OR name LIKE '%s';
```

Fetch names of cities that start with any letter followed by 'ublin' (like Dublin in Ireland or Lublin in Poland):

```sql
SELECT name
FROM city
WHERE name LIKE '_ublin';
```

#### OTHER OPERATORS

Fetch names of cities that have a population between 500K and 5M:

```sql
SELECT name
FROM city
WHERE population BETWEEN 500000 AND 5000000;
```

Fetch names of cities that don't miss a rating value:

```sql
SELECT name
FROM city
WHERE rating IS NOT NULL;
```

Fetch names of cities that are in countries with IDs 1, 4, 7, or 8:

```sql
SELECT name
FROM city
WHERE country_id IN (1, 4, 7, 8);
```

### QUERYING MULTIPLE TABLES

#### INNER JOIN

**`JOIN`** (or explicitly **`INNER JOIN`**) returns rows that have matching values in both tables.

```sql
SELECT city.name, country.name
FROM city
[INNER] JOIN country
  ON city.country_id = country.id;
```

#### LEFT JOIN

**`LEFT JOIN`** returns all rows from the left table with corresponding rows from the right table. If there's no matching row, **`NULL`**s are returned as values from the second table.

```sql
SELECT city.name, country.name
FROM city
LEFT JOIN country
  ON city.country_id = country.id;
```

#### RIGHT JOIN

**`[RIGHT JOIN](https://learnsql.com/blog/right-join/)`** returns all rows from the right table with corresponding rows from the left table. If there's no matching row, **`NULL`**s are returned as values from the left table.

```sql
SELECT city.name, country.name
FROM city
RIGHT JOIN country
  ON city.country_id = country.id;
```

#### FULL JOIN

**`FULL JOIN`** (or explicitly **`FULL OUTER JOIN`**) returns all rows from both tables – if there's no matching row in the second table, **`NULL`**s are returned.

```sql
SELECT city.name, country.name
FROM city
FULL [OUTER] JOIN country
  ON city.country_id = country.id;
```

#### CROSS JOIN

**`CROSS JOIN`** returns all possible combinations of rows from both tables. There are two syntaxes available.

```sql
SELECT city.name, country.name
FROM city
CROSS JOIN country;
```

```sql
SELECT city.name, country.name
FROM city, country;
```

#### NATURAL JOIN

**`NATURAL JOIN`** will join tables by all columns with the same name.

```sql
SELECT city.name, country.name
FROM city
NATURAL JOIN country;
```

**`NATURAL JOIN`** used these columns to match rows: **`city.id`**, **`city.name`**, **`country.id`**, **`country.name`**.  
**`NATURAL JOIN`** is very rarely used in practice.

### AGGREGATION AND GROUPING

`GROUP BY` **groups** together rows that have the same values in specified columns. It computes summaries (aggregates) for each unique combination of values.

#### AGGREGATE FUNCTIONS

- `avg(expr)` − average value for rows within the group
- `count(expr)` − count of values for rows within the group
- `max(expr)` − maximum value within the group
- `min(expr)` − minimum value within the group
- `sum(expr)` − sum of values within the group

#### TOP PREDICATE

Select certain number or certain percentage of records retrieve top 5 most expensive products.
```sql
SELECT TOP 5 ProductName, UnitPrice
FROM Products
ORDER BY UnitPrice DESC;
```

Retrieve top 10 percent most expensive products
```sql
SELECT TOP 10 PERCENT ProductName, UnitPrice
FROM Products
ORDER BY UnitPrice DESC;
```

List top 5 customers who created the most total revenue.
```sql
SELECT
	TOP 5 c.CustomerId,
	c.ContactName,
	SUM(od.UnitPrice * od.Quantity) As SumRevenue
FROM Customers c
	JOIN Orders o ON c.CustomerId = o.CustomerId
	JOIN [Order Details] od ON o.OrderId = od.OrderId
GROUP BY c.CustomerId, c.ContactName
ORDER BY SumRevenue DESC;
```

### SUBQUERIES

A subquery is a query that is nested inside another query, or inside another subquery. There are different types of subqueries.

#### SINGLE VALUE

The simplest subquery returns exactly one column and exactly one row. It can be used with comparison operators `=`, `<`, `<=`, `>`, or `>=`.

This query finds cities with the same rating as Paris:

```sql
SELECT name
FROM city
WHERE rating = (
  SELECT rating
  FROM city
  WHERE name = 'Paris'
);
```

#### MULTIPLE VALUES

A subquery can also return multiple columns or multiple rows. Such subqueries can be used with operators `IN`, `EXISTS`, `ALL`, or `ANY`.

This query finds cities in countries that have a population above 20M:

```sql
SELECT name
FROM city
WHERE country_id IN (
  SELECT country_id
  FROM country
  WHERE population > 20000000
);
```

#### CORRELATED

A correlated subquery refers to the tables introduced in the outer query. A correlated subquery depends on the outer query. It cannot be run independently from the outer query.

This query finds cities with a population greater than the average population in the country:

```sql
SELECT *
FROM city main_city
WHERE population > (
  SELECT AVG(population)
  FROM city average_city
  WHERE average_city.country_id = main_city.country_id
);
```

This query finds countries that have at least one city:

```sql
SELECT name
FROM country
WHERE EXISTS (
  SELECT *
  FROM city
  WHERE country_id = country.id
);
```

### SET OPERATIONS

Set operations are used to combine the results of two or more queries into a single result. The combined queries must return the same number of columns and compatible data types. The names of the corresponding columns can be different

#### UNION

**`UNION`** combines the results of two result sets and removes duplicates. **`UNION ALL`** doesn't remove duplicate rows.

This query displays German cyclists together with German skaters:

```sql
SELECT name
FROM cycling
WHERE country = 'DE'
UNION / UNION ALL
SELECT name
FROM skating
WHERE country = 'DE';
```

#### Differences

1. **`UNION`** will remove duplicate values but **`UNION ALL`** will not
2. If you use **`UNION`**, the records from the first column will be sorted ascendingly automatically.
3. **`UNION`** can not be used in recursive CTE but **`UNION ALL`** can.

### Window Function

Window function operated on a set of rows and returns a single aggregated value for each and every row by adding an extra column.

#### RANK()

Give a rank based on a certain order, when there is a tie, there will be a value gap

```sql
SELECT
	ProductId,
	ProductName,
	UnitPrice,
	RANK() OVER(ORDER BY UnitPrice DESC) RNK
FROM Products;
```

Product with the 2nd highest price
```sql
SELECT
	dt.ProductId,
	dt.ProductName,
	dt.UnitPrice,
	dt.RNk
FROM (
	SELECT 
		ProductId,
		ProductName,
		UnitPrice,
		RANK() OVER(ORDER BY UnitPrice DESC) RNK
	FROM Products
) dt
WHERE dt.RNk = 2
```

#### DENSE_RANK()

If you do not want the value gap, use `DENSE_RANK()`
```sql
SELECT
	ProductId,
	ProductName,
	UnitPrice,
	RANK() OVER(ORDER BY UnitPrice DESC) RNK,
	DENSE_RANK() OVER(ORDER BY UnitPrice DESC) DENSE_RANK
FROM Products;
```

#### ROW_NUMBER()

It will return the ranking of the sorted record starting from 1
```sql
SELECT
	ProductId,
	ProductName,
	UnitPrice,
	RANK() OVER(ORDER BY UnitPrice DESC) RNK,
	DENSE_RANK() OVER(ORDER BY UnitPrice DESC) DENSE_RANK,
	ROW_NUMBER() OVER(ORDER BY UnitPrice DESC) RowNum
FROM Products;
```

#### PARTITION BY

It divides the result set into partitions and perfrom calculations on each subset. it is always used in conjuction with the window function
  
List customers from every country with the ranking for number of orders
```sql
SELECT
	c.ContactName,
	c.Country,
	COUNT(O.OrderId) AS NumofOrders,
	RANK() OVER (
		PARTITION BY c.Country
		ORDER BY COUNT(O.OrderId) DESC
	) RNK
FROM Customers c
	JOIN Orders o On c.CustomerId = o.CustomerId
GROUP BY c.ContactName, c.Country;
```

Find top 3 customers from every country with maximum orders
```sql
SELECT
	dt.ContactName,
	dt.Country,
	dt.NumOfOrders,
	dt.RNK
FROM (
	SELECT
		c.ContactName,
		c.Country,
		COUNT(O.OrderId) AS NumofOrders,
		RANK() OVER (
			PARTITION BY c.Country
			ORDER BY COUNT(O.OrderId) DESC
		) RNK
	FROM Customers c
		JOIN Orders o On c.CustomerId = o.CustomerId
	GROUP BY c.ContactName, c.Country
) dt
WHERE dt.RNK <=3
```

### Common Table Expression (CTE)

A temporary name result set to make our query more readable.

```sql
WITH OrderCntCTE AS (
	SELECT
		CustomerId,
		Count(OrderId) As TotalNumOfOrders
	FROM Orders
	GROUP BY CustomerId
)
SELECT
	c.ContactName,
	c.City,
	c.Country,
	cte.TotalNumOfOrders
FROM Customers c LEFT
	JOIN OrderCntCTE cte ON c.CustomerId = cte.CustomerID;
```

**Lifecycle**: it has to be used to used in the next select statement right away; have to be created and used in a single batch.

**Recursive CTE**: if we have a CTE that calls itself recursively, that is called recursive CTE. The true power of CTE is that it can call itself recursively
```sql
WITH EmpHierarchyCTE AS (
	SELECT EmployeeId, FirstName, ReportsTo, 1 level
	FROM Employees
	WHERE ReportsTo is null
	UNION ALL
	SELECT e.EmployeeId, e.FirstName, e.ReportsTo, cte.level + 1
	FROM Employees e
		INNER JOIN EmpHierarchyCTE cte ON e.ReportsTo = cte.EmployeeId
)
SELECT * FROM EmpHierarchyCTE;
```

### Managing SQL constraints![Copy Icon](https://www.cockroachlabs.com/images/icons/copy-icon.svg)

#### [ADD CONSTRAINT](https://www.cockroachlabs.com/docs/stable/alter-table#add-constraint)

Add a key, check, or unique constraint to a column.

```sql
ALTER TABLE users
ADD CONSTRAINT id_name_unique UNIQUE (id, name);
```

#### [DROP CONSTRAINT](https://www.cockroachlabs.com/docs/stable/alter-table#drop-constraint)

Remove a constraint from a column.

```sql
ALTER TABLE users
DROP CONSTRAINT id_name_unique;
```

#### [ALTER COLUMN](https://www.cockroachlabs.com/docs/stable/alter-table#alter-column)

Add or remove `DEFAULT` and `NOT NULL` constraints, change datatypes.

```sql
ALTER TABLE subscriptions
ALTER COLUMN newsletter SET NOT NULL;
```

#### PRIMARY KEY constraint

```sql
CREATE TABLE projects (
    project_id INT PRIMARY KEY,
    project_name VARCHAR(255),
    start_date DATE NOT NULL,
    end_date DATE NOT NULL
);
```

```sql
CREATE TABLE projects (
    project_id INT,
    project_name VARCHAR(255),
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    CONSTRAINT pk_id PRIMARY KEY (project_id)
);
```

Adding the primary key with ALTER TABLE statement.
```sql
ALTER TABLE project_milestones
ADD CONSTRAINT pk_milestone_id PRIMARY KEY (milestone_id);
```

You can skip the `CONSTRAINT` clause as follows:
```sql
ALTER TABLE project_milestones
ADD PRIMARY KEY (milestone_id);
```

#### FOREIGN KEY constraint

A foreign key is a column or a group of columns that enforces a link between the data in two tables.

```sql
CREATE TABLE projects (
    project_id INT AUTO_INCREMENT PRIMARY KEY,
    project_name VARCHAR(255),
    start_date DATE NOT NULL,
    end_date DATE NOT NULL
);

CREATE TABLE project_milestones (
    milestone_id INT AUTO_INCREMENT PRIMARY KEY,
    project_id INT,
    milestone_name VARCHAR(100),
    FOREIGN KEY (project_id) REFERENCES projects (project_id)
);
```

You can assign a name to a FOREIGN KEY constraint as follows:
```sql
CREATE TABLE project_milestones (
    milestone_id INT AUTO_INCREMENT PRIMARY KEY,
    project_id INT,
    milestone_name VARCHAR(100),
    CONSTRAINT fk_project FOREIGN KEY (project_id)
        REFERENCES projects (project_id)
);
```

To add a FOREIGN KEY constraint to existing table, you use the [ALTER TABLE](https://www.sqltutorial.org/sql-alter-table/) statement.
```sql
ALTER TABLE table_1
ADD CONSTRAINT fk_name FOREIGN KEY (fk_key_column)
   REFERENCES table_2(pk_key_column)
```

### Inserting data![Copy Icon](https://www.cockroachlabs.com/images/icons/copy-icon.svg)

#### [INSERT INTO … VALUES](https://www.cockroachlabs.com/docs/stable/insert)

Insert rows with specified values into a table.

```sql
INSERT INTO users (name, city)
VALUES ('Alice', 'New York');
```
#### [INSERT INTO … SELECT](https://www.cockroachlabs.com/docs/stable/insert#insert-from-a-select-statement)

Insert rows into a table from the results of a query.

```sql
INSERT INTO drivers (id, city, name, address)
SELECT id, city, name, address
FROM users
WHERE name IN ('Anita Atkinson', 'Devin Jordan');
```

## Working with your data![Copy Icon](https://www.cockroachlabs.com/images/icons/copy-icon.svg)

### Modifying data![Copy Icon](https://www.cockroachlabs.com/images/icons/copy-icon.svg)

#### [UPDATE](https://www.cockroachlabs.com/docs/stable/update)

Update row(s) in a table.

```sql
UPDATE users
SET address = '201 E Randolph St'
WHERE id = '851eb851-eb85-4000-8000-00000000001a';
```

Note: without a `WHERE` statement, `UPDATE` will update the value of the specified column or columns for **all rows**.

#### [INSERT INTO … ON CONFLICT](https://www.cockroachlabs.com/docs/stable/update-data#use-insert-on-conflict)

Insert a new row, or perform a different action if a conflict with an existing row is detected (i.e., an “upsert”).

```sql
INSERT INTO employees (id, name, email)
VALUES (2, ‘Dennis’, ‘dennisp@weyland.corp’)
ON CONFLICT (id) DO UPDATE;
```

#### [UPSERT](https://www.cockroachlabs.com/docs/stable/upsert)*

Upsert a row into the database.

```sql
UPSERT INTO employees (id, name, email)
VALUES (6, ‘Lambert’, ‘lambert@weyland.corp`);
```

#### [DELETE FROM](https://www.cockroachlabs.com/docs/stable/delete)

Delete a specific row or rows.

```sql
DELETE FROM promo_codes
WHERE code = 'HAPPY50';
```

## Managing indexes![Copy Icon](https://www.cockroachlabs.com/images/icons/copy-icon.svg)

#### [CREATE INDEX](https://www.cockroachlabs.com/docs/stable/create-index)

Create an index for a table using one or more columns.

```sql
CREATE INDEX ON table1 (column1, column2);
```
#### [ALTER INDEX … RENAME TO](https://www.cockroachlabs.com/docs/stable/alter-index#rename-to)

Rename an index.

```sql
ALTER INDEX usersname_idx
RENAME TO users_name_idx;
```
``
#### [DROP INDEX](https://www.cockroachlabs.com/docs/stable/drop-index)

Remove an index.

```sql
DROP INDEX users_name_idx;
```

## Managing Views

Create a new view that consists  of c1 and c2

```sql
CREATE VIEW v(c1,c2) AS
SELECT c1, c2 FROM t;
```

Create a new view with check option

```sql
CREATE VIEW v(c1,c2) AS
SELECT c1, c2 FROM t;
WITH [CASCADED | LOCAL] CHECK OPTION;
```

Create a recursive view

```sql
CREATE RECURSIVE VIEW v AS
select-statement -- anchor part
UNION [ALL]
select-statement; -- recursive part
```

Create a temporary view

```sql
CREATE TEMPORARY VIEW v AS
SELECT c1, c2 FROM t;
```

Delete a view

```sql
DROP VIEW view_name;
```

## Transactions in SQL

### BEGIN TRANSACTION: Start a New Transaction

```sql
BEGIN TRANSACTION;
```

This statement starts a new [transaction](https://www.geeksforgeeks.org/sql-transactions/).

### COMMIT: Save Changes Made During the Current Transaction

```sql
COMMIT;
```

This statement saves all changes made during the current transaction.

### ROLLBACK: Undo Changes Made During the Current Transaction

```sql
ROLLBACK;
```

There 3 modes of transaction:
- Autocommit transaction
- Implicit transaction
- Explicit transaction: you have to explicitly specify the starting and ending points of the transaction

## ACID Properties

1. Atomicity: work most be atomic
2. Consistency: a database is transformed from one consistent state to another consistent state
3. Isolation: two transactions will be isolated from each other by locking the resource
4. Durability: once the transaction is completed, the changes that we make to database will be permanent

## Concurrency Problem

1. **Dirty read**: if transaction 1 allows transaction 2 to read the uncommitted data but transaction 1 rolls back. happens when isolation level is read uncommitted and is solved by updating isolation level to read committed

2. **Lost update**: when tran1 and tran2 are trying to read and update the same data but tran2 finished its work earlier even though tran1 started the transaction first and as a result the update from tran2 will be missing. 
   
   It happens when isolation level is read committed and is solved by updating the isolation level to repeatable read

3. **Non repeatable read**: happens when t1 reads the same data twice but t2 is updating the data; happens when isolation level is read committed and is solved by updating the isolation level to repeatable read

4. **Phantom read**: happens when t1 read the same data twice while t2 is inserting the data; happens when isolation level is set to repeatable read and is solved by updating the isolation level to serializable

## SQL Execution Order

**`SELECT`** fields, aggregate(fields)

**`FROM`** table **`JOIN`** table2 **`ON`** ...

**`WHERE`** criteri  --- optional

**`GROUP BY`** fields  --- use when we have both aggregated and non aggregated fields

**`HAVING`** criteria  --optional

**`ORDER BY`** by fields **`DESC`**  -- optional

FROM/JOIN ---> WHERE ---> GROUP BY ---> HAVING ---> SELECT ---> DISTINCT ---> ORDER BY

### `TRUNCATE` vs. `DELETE`

1. `DELETE` is a DML. So it will not reset the property value. `TRUNCATE` is DDL so it will reset the property value
2. `DELETE` can be used with `WHERE` clause but `TRUNCATE` can not be

### DROP 

`DROP` is a DDL statement that will delete the whole table.

### PERFORMANCE TUNING

1. You need to look at the execution plan; sql profiler
2. create an index wisely.
3. avoid unnecessary joins.
4. Avoid using select *
5. use a derived table to avoid grouping of lots of non-aggregated fields.
6. replace subquery with join if needed.
