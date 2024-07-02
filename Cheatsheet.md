# SQL Interview Questions

  

1. What is index; types of indices; pros and cons

  

- index is a data structure that improves the speed of data retrieval operations on a database table

- types of indices: clustered index, non-clustered index

- pros: faster data retrieval, faster data sorting, faster data searching

- cons: slower DML operations, increased storage space

  

2. What's the difference between Primary key and Unique constraint?

  

- primary key: unique identifier for a row in a table, cannot be null, can only have one primary key per table, automatically sorted

- unique constraint: ensures that all values in a column are unique, can be null, can have multiple unique constraints per table, not automatically sorted

  

3. Tell me about check constraint

  

- check constraint is used to limit the range of values that can be placed in a column

  

4. Difference between temp table and table variable

  

- temp table: created in tempdb, can have indexes, statistics, and constraints, can be used in transactions

- table variable: created in memory, cannot have indexes, statistics, or constraints, cannot be used in transactions

  

5. Difference between WHERE and HAVING

  

- WHERE is used to filter rows before grouping

- HAVING is used to filter rows after grouping

  

6. Difference between RANK() and DenseRank() — value gap

  

- RANK(): assigns a unique rank to each distinct row, leaving gaps in the ranking sequence

- DENSE_RANK(): assigns a unique rank to each distinct row, leaving no gaps in the ranking sequence

  

7. COUNT(*) vs. COUNT(colName)

  

- COUNT(*): counts all rows in a table

- COUNT(colName): counts the number of non-null values in a column

  

8. What's the difference between left join and inner join? JOIN and Subquery, which one has a better performance, why?

  

- left join: returns all rows from the left table and the matched rows from the right table

- inner join: returns only the rows that have matching values in both tables

- JOIN and Subquery: JOIN has better performance because it has built-in optimzation which makes it more efficient than a subquery

  

9. What is correlated subquery

  

- correlated subquery is a subquery that depends on the outer query

  

10. What is a CTE, why do we need CTE?

  

- CTE (Common Table Expression) is a temporary result set that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement

  

11. What does SQL Profiler do?

  

- SQL Profiler is a tool used to monitor and analyze the performance of SQL queries

  

12. What is SQL injection, how to avoid SQL injection?

  

- SQL injection is a type of attack that allows an attacker to execute malicious SQL statements

- to avoid SQL injection, use parameterized queries, stored procedures, and input validation

  

13. Difference between SP and user defined function? When to use SP when to use function?

  

- stored procedure: can return multiple values, cannot be used in a SELECT statement, can have input and output parameters

- user-defined function: returns a single value, can be used in a SELECT statement, cannot have output parameters

  

14. Criteria of Union and Union all? Difference between UNION and UNION ALL

  

- UNION: removes duplicate rows, can be use recursively

- UNION ALL: does not remove duplicate rows

  

15. Steps you take to improve SQL Queries

  

- use indexes

- avoid using SELECT *

- use parameterized queries

- avoid using subqueries

  

16. concurrency problem in transaction

  

- dirty read: reading uncommitted data, can be prevented by using isolation levels like READ COMMITTED

- lost update: overwriting uncommitted data, can be prevented by using locking mechanisms

- non-repeatable read: reading different values for the same row in the same transaction, can be prevented by using isolation levels like REPEATABLE READ

- phantom read: reading different rows for the same query in the same transaction, can be prevented by using isolation levels like SERIALIZABLE

  

17. what is deadlock, how to prevent

  

- deadlock is a situation where two or more transactions are waiting for each other to release locks

  

18. what is normalization, 1NF, benefits using normalization

  

- normalization is the process of organizing data in a database

- 1NF: each column in a table must be atomic, no repeating groups, no multi-valued attributes

- 2NF: each non-key column must be fully functionally dependent on the primary key

- 3NF: each non-key column must be non-transitively dependent on the primary key

- benefits of normalization: reduces data redundancy, improves data integrity, improves data consistency

  

19. what are the system defined databases?

  

- master: contains system information

- model: used as a template for new databases

- msdb: used by SQL Server Agent for scheduling jobs

- tempdb: used for temporary storage

- resource: read-only database that contains system objects

  

20. composite key

  

- composite key is a key that consists of multiple columns

  

21. candidate key

  

- candidate key is a key that uniquely identifies a row in a table

  

22. DDL vs. DML

  

- DDL (Data Definition Language): used to define the structure of a database, includes CREATE, ALTER, DROP

- DML (Data Manipulation Language): used to manipulate data in a database, includes SELECT, INSERT, UPDATE, DELETE

  

23. ACID property

  

- Atomicity: transactions should be atomic, all or nothing

- Consistency: data must be consistent before and after a transaction

- Isolation: transactions should be isolated from each other

- Durability: changes made by a transaction should be permanent

  

24. table scan vs. index scan

  

- table scan: scans the entire table to find the required data

- index scan: scans the index to find the required data

  

25. Difference between Union and JOIN

  

- UNION: combines the results of two or more SELECT statements into a single result set vertically

- JOIN: combines the rows from two or more tables based on a related column, horizontally

  

26. Examples of one-one, one-many, many-many relationships; how can we create such relationships in db

  

- one-one: student and student details

- one-many: department and employees

- many-many: students and courses

  

# C# Interview Questions

  

1. reference type vs. value type

  

- value type is stored in stack, it is a direct value

- reference type is stored in heap, it is a reference to the value

  

2. boxing vs. unboxing

  

- boxing is converting a value type to a reference type

- unboxing is converting a reference type to a value type

  

3. walk us through the four principles of OOP with examples, focus on what does the principle mean, why do we need to use that, examples of us that

  

- encapsulation: hide the implementation details, only expose the necessary information to the outside world

- inheritance: ability to create a new class from an existing class, reuse the code

- polymorphism: ability to take multiple forms, overriding is runtime polymorphism, overloading is compile time polymorphism

- abstraction: hide the unnecessary details, only show the necessary information

  

1. different access modifiers

  

- public: accessible from anywhere

- private: only accessible within the class

- protected: accessible within the class and its derived classes

- internal: accessible within the same assembly

  

2. overriding vs. overloading, which one is runtime and which one is compile time

  

- overriding is runtime polymorphism, overloading is compile time polymorphism

  

3. can we have multiple inheritance in C#

  

- no, C# only supports single inheritance, but we can use interfaces to achieve multiple inheritance

  

4. virtual method vs. abstract method

  

- virtual method has a default implementation, can be overridden in the derived class

- abstract method does not have a default implementation, must be implemented in the derived class

  

5. difference between abstract class and interface, when to use which one

  

- abstract class can have both abstract and non-abstract methods, can have fields, properties, and constructors

- interface can only have abstract methods, properties, and events, no fields, no constructors

- use abstract class when you want to provide a default implementation, use interface when you want to provide a contract

  

4. What does constructor do in a class? Can it be overridden? Can it be overloaded?

  

- constructor is a special method that is called when an instance of a class is created

- constructor can be overloaded, but it cannot be overridden

  

5. What does static keyword do in C#?

  

- static keyword is used to declare a member that belongs to the type itself, rather than to any instance of the type

  

6. what are delegates in C#, what are different types of built-in delegates

  

- delegates are type-safe function pointers

- Action: delegate that takes no parameters and returns void

- Predicate: delegate that takes one parameter and returns a boolean

- Func: delegate that takes one or more parameters and returns a generic type

  

7. What is the extension method in C#? examples of built-in extension methods? How to create custom extension methods?

  

- extension method is a static method that can be called as if it were an instance method of the extended type

- LINQ methods like Where(), Select(), OrderBy()

  

```csharp

public static class StringExtensions

{

public static string Reverse(this string str)

{

char[] charArray = str.ToCharArray();

Array.Reverse(charArray);

return new string(charArray);

}

}

```

  

8. Ref vs. Out vs. Params

  

- ref: used to pass a variable as a reference, must be initialized before passing

- out: used to return multiple values from a method, does not need to be initialized before passing

- params: used to pass a variable number of arguments to a method

  

9. Pass by reference vs. Pass by Value

  

- pass by reference: passing the reference of the variable, changes made to the parameter inside the method will affect the original variable

- pass by value: passing the value of the variable, changes made to the parameter inside the method will not affect the original variable

  

10. array vs. arrayList

  

- array: fixed size, strongly typed, faster

- arrayList: dynamic size, can store different types, slower

  

11. how do you handle exceptions? Syntax.

  

```csharp

try

{

// code that may throw an exception

}

catch (Exception ex)

{

// handle the exception

}

finally

{

// cleanup code

}

```

  

12. what is generic, syntax to define, how can we limit the implementation of generics

  

```csharp

public class GenericClass<T>

{

public T Value { get; set; }

}

  

// limit the implementation of generics

public class GenericClass<T> where T : class

{

public T Value { get; set; }

}

```

  

13. Generic Collection vs. non-generic collection

  

- generic collection is type-safe

- non-generic collection is not type-safe

  

14. What is LINQ, why use it

  

- LINQ (Language Integrated Query) is a set of methods to query data from different data sources

  

15. IEnumreable vs. IQuerable

  

- IEnumerable is the base interface for all collections in LINQ

- IQueryable extends IEnumerable, is used for querying data from a database

  

16. First, FirstOrDefault, Single, SingleOrDefault

  

- First: returns the first element of a sequence

- FirstOrDefault: returns the first element of a sequence or a default value if the sequence is empty

- Single: returns the only element of a sequence

- SingleOrDefault: returns the only element of a sequence or a default value if the sequence is empty or contains more than one element

  

17. Any() vs. All()

  

- Any: returns true if any element in a sequence satisfies a condition

- All: returns true if all elements in a sequence satisfy a condition

  

18. How to implement pagination in LINQ (answer is to use Skip() and Take())

  

```csharp

var query = context.Products.OrderBy(p => p.Name).Skip(10).Take(5);

```

  

19. Deferred Execution and Immediate Execution

  

- Deferred Execution: queries are not executed until the result is enumerated

- Immediate Execution: queries are executed immediately