## View

A **view** is a virtual table that is created by a query joining one or more tables. It is a stored query that users can query just like they would a table. The view itself does not store data; rather, it dynamically retrieves data from the underlying tables whenever it is accessed.

### Benefits

1. **Simplified Data Access:**
	- **Abstraction**: Views can abstract complex queries involving joins and subqueries, making it easier for users to access and manipulate data without needing to understand the underlying query logic.
	- **User-Friendly**: Provides a simplified interface for users, presenting only relevant data.
1. **Security**:
    - **Access Control**: Views can restrict access to sensitive data. By granting permissions on views rather than tables, you can control which parts of the data a user can see and manipulate.
    - **Column Masking**: Views can hide certain columns from users who don’t need to see them.
2. **Data Consistency**:
    - **Centralized Logic**: If you have a complex business logic that is reused across multiple queries, putting it into a view ensures consistency and reduces redundancy.
    - **Up-to-Date Data**: Since views retrieve the latest data from the underlying tables, they always provide an up-to-date view of the data without needing to refresh or maintain separate copies.
3. **Reusability**:
    - **Reusable Queries**: Views can be reused in multiple queries, reducing the need to rewrite complex SQL code.
    - **Modular Design**: Encourages a modular approach to database design, where complex queries can be broken down into simpler, reusable views.
4. **Data Aggregation**:
    - **Pre-Aggregated Data**: Views can be used to present aggregated data (such as sums, averages, counts) which can improve performance by reducing the need for repetitive aggregation calculations.
5. **Logical Data Independence**:
    - **Schema Evolution**: Changes to the underlying table structures do not necessarily affect the views, providing a layer of abstraction that can insulate users and applications from schema changes.
6. **Improved Performance**:
    - **Materialized Views**: While standard views do not store data, materialized views do store the result set of the query. This can significantly improve performance for complex queries that do not change frequently.

### Example

```sql
CREATE VIEW EmployeeSales AS
SELECT e.EmployeeID, e.FirstName, e.LastName, s.TotalSales
FROM Employees e
JOIN Sales s ON e.EmployeeID = s.EmployeeID
WHERE s.TotalSales > 10000;
```

This view, named `EmployeeSales`, presents a simplified and filtered view of the data, showing only employees with total sales greater than 10,000.

## Stored Procedure

A **stored procedure** is a precompiled collection of one or more SQL statements stored on the database server. They are executed as a single unit and can be called by applications or other SQL code. Stored procedures can accept parameters, perform operations (such as insert, update, delete, or select), and return results.

### Benefits
- **Performance**:
    - **Reduced Network Traffic**: By bundling multiple SQL statements into a single procedure, stored procedures reduce the amount of data transmitted over the network.
    - **Precompilation**: Stored procedures are precompiled and optimized by the database server, resulting in faster execution compared to sending individual SQL statements.
- **Security**:
    - **Controlled Access**: You can grant users permission to execute a stored procedure without giving them direct access to the underlying tables.
    - **SQL Injection Protection**: By using parameters, stored procedures can help prevent SQL injection attacks.
- **Maintainability**:
    - **Centralized Logic**: Business logic can be centralized in stored procedures, making it easier to manage and update.
    - **Code Reusability**: Stored procedures can be reused across different applications and parts of the database, reducing redundancy.
- **Consistency**:
    - **Uniform Implementation**: Ensures consistent implementation of business rules and validation logic across different applications.
    - **Transaction Management**: Stored procedures can manage transactions, ensuring that a series of operations either complete successfully or fail together.
- **Modularity**:
    - **Separation of Concerns**: Complex operations can be broken down into simpler, modular stored procedures, improving code organization and readability.
- **Enhanced Functionality**:
    - **Complex Operations**: Stored procedures can include complex control-of-flow logic, such as loops and conditionals, which are not possible with standard SQL statements.
    - **Error Handling**: Provides mechanisms for error handling and logging, which can help in diagnosing issues.

### Examples

Stored procedure with input:
```sql
CREATE PROC SpAddNumbers
@a INT,
@b INT
AS
PRINT @a + @b 

EXEC SpAddNumbers 10, 20
```

Stored procedure with output:
```sql
CREATE PROC SpGetName
@id int,
@EName varchar(20) OUT
AS
BEGIN
SELECT @EName = EName
FROM Employee
WHERE Id = @id
END

BEGIN
DECLARE @en VARCHAR(20)
EXEC spGetName 2, @en OUT
PRINT @en
END
```

Stored procedure which returns table:
```sql
CREATE PROC spGetAllEmp
AS
BEGIN
SELECT *
FROM Employee
END

EXEC spGetAllEmp
```

## Function

Function can be only used in a SQL statement, mostly in a select statement, or representing a data or a dataset 15.

- Aggregate functions  
- Analytic functions  
- Ranking functions  
- Rowset functions  
- Scalar functions  

## Trigger

Triggers are a special type of stored procedure that get executed (fired) when a specific event happens. 
- DDL trigger
- DML trigger
- LogOn trigger

## Temporary table
- **Local Temp Table:** As the name suggests, it is “local” scope meaning that it is only accessible in the session that it was created. Needs an identifier of “#”
- **Global Temp Tables:** Any user with proper permissions access to the current database they are in have access to the table. Unlike local temporary tables, you can’t create simultaneous versions of a global temporary table, as this will generate a naming conflict. Needs an identifier of “##”

### Syntax
```sql
CREATE TABLE #LocalTemp(
column_name1 column_data_type1,
column_name2 column_data_type2)

INSERT (INTO) #LocalTemp VALUES (value1, value 2), (value3, value 4)
-- OR
INSERT (INTO) #LocalTemp SELECT field1, field2, field3 FROM SampleTable

-- the (Into) is optional

-- another way is using Select -> Into

SELECT * INTO #CopyOfProducts FROM Products
```

## Variable

A **variable** is a data type that can be used within a Transact-SQL batch, stored procedure, or function — and is created and defined similarly to a table, only with a strictly defined lifetime scope.

### Reasons to use
- Temporary tables causes performance issues
- Temporary tables may cause unwanted disk overhead in tempdb, locking of tempdb during their creation, as well as cause stored procedure recompilations, when included within a stored procedure’s definition
- Microsoft recommends table variables as a replacement of temporary tables when the data set is not very large. However, table variables performance suffers when the result set becomes too large
- Shorter locking periods (because of the tighter scope)

### Syntax
```sql
DECLARE @TableName TABLE (column_name1 column_data_type1)

INSERT (INTO) @TableName VALUES (value1, value 2), (value3, value 4)
-- OR
INSERT (INTO) @TableName SELECT field1, field2, field3 FROM SampleTable
```

### Temp tables vs. table variables
1. **Storage:** both Temp Tables and Table Variables are stored in tempDb
2. **Scope:** Temp Tables scoped local/global; Table Variables scoped for current batch
3. Temp Tables for large data; Table Variables for smaller data 
4. **Usage:** Temp Tables not in Stored Procedure, Functions; Table Variables can be used 
5. **Structure:** Temp Tables can create index/ constraints except Foreign key; Table Variables cannot

## Normalization

### First Normal Form  
It’s all about atomic values:
- One cell, one value
- No repeating groups

### Second Normal Form  
First Normal Form + No Partial Dependency

### Third Normal Form  
Second Normal Form + No Transitive Dependency