# C# Types and Concepts

## Categories of Types

### Built-in Types

1. **Signed types:** Can represent both positive and negative values.
2. **Unsigned types:** Can only represent positive values.

### User-Defined Types

- Types created by the user using `struct`, `class`, `enum`, `interface`, etc.

## Object Type

- The base type for all other types in C#.

## Another Categorization of Types

### 1. Value Types

- Directly hold their values.
- Stored in stack memory.
- Not collected by garbage collector.
- Created using `struct` or `enum`.
- Cannot accept null values.

### 2. Reference Types

- Hold the memory address (reference) for their values.
- Stored in heap memory.
- Collected by garbage collector.
- Created using `class`, `interface`, `delegate`, or array.
- Can accept null values.

## Value Type vs Reference Type

1. **Storage:**
   - Value type: Stored in stack memory.
   - Reference type: Stored in heap memory.
2. **Garbage Collection:**
   - Value type: Not collected by garbage collector.
   - Reference type: Collected by garbage collector.
3. **Creation:**
   - Value type: Created by `struct` or `enum`.
   - Reference type: Created by `class`, `interface`, `delegate`, or array.
4. **Nullability:**
   - Value type: Cannot accept null values.
   - Reference type: Can accept null values.

## CLR: Common Language Runtime

- The runtime environment for executing .NET applications.

## Heap Memory

- **Managed heap:** Managed by the garbage collector.
- **Unmanaged heap:** Used for unmanaged resources like database connections, file transmission, etc.; must be manually cleared.

### Garbage Collector

- Manages heap memory, which is divided into three generations: 0, 1, and 2.

## Enum

- Enumeration; a value type.
- Used when the values are known, small, and specific.

## Method Syntax

```csharp
[Access Modifiers] ReturnType MethodName([Formal Parameters]){
   // Method body
}
```

### Access Modifiers

1. **Public:** Members can be accessed anywhere.
2. **Private:** Members can be accessed only in the current class.
3. **Protected:** Members can be accessed in the current class and derived classes.
4. **Internal:** Members can be accessed in the current assembly.

## Assembly

- A compiled unit of executable code.
- When a project compiles, it turns into an assembly, which will become a `.dll` or `.exe` file.

## Parameters

1. **Pass by Value:** A copy of the actual parameter is created and passed to the formal parameters; default mode.
2. **Pass by Reference:** A reference of the actual parameter is passed to the formal parameters; changes in formal parameters will be reflected in actual parameters.
3. **Optional Parameters:** Allows defining default values for method parameters.
4. **Out Mode:** Used when you want to return more than one value from a single method.
5. **Params:** Used to pass parameters of the same type but with variable length.

## Boxing and Unboxing

- **Boxing:** Conversion of value type to reference type.
- **Unboxing:** Conversion of reference type to value type.

## Ref vs Out

1. **Initialization:**
   - `ref`: The value must be initialized before passing.
   - `out`: The value does not need to be initialized before passing.
2. **Behavior:**
   - Both are pass-by-reference and will change the actual value of the variable.

This structured markdown format provides a clear overview of the C# types and concepts, with corrections and proper organization.

# C# OOP Concepts and Advanced Topics

## Encapsulation
- **Definition:** Hides the data implementation and provides flexibility.
  
## Constructor

1. **Definition:** A special method that has the same name as the class and does not have any return type, not even `void`.
2. **Purpose:** Used to create an object of the class and initialize class members.
3. **Default Constructor:** If no constructor is defined in the class, the C# compiler provides a default parameterless constructor.
4. **Overloading:** Constructors can be overloaded, meaning they can have the same name but different parameters.
5. **Inheritance:** Constructors cannot be inherited or overridden.
6. **Base Class Call:** By default, a derived class constructor will call the base class constructor.

## Inheritance

- **Definition:** Allows one class to inherit from another existing class so that the derived class can reuse, extend, and modify the code from the base class.
- **Note:** C# supports single inheritance.

### Example: Employee Management System
- **Full-time Employee:** Biweekly pay, benefits.
- **Part-time Employee:** Hourly pay.
- **Common Attributes:** id, name, phone, email, address; perform work.

## Abstract Class

- **Definition:** Cannot create an instance of this class; can contain both abstract and concrete methods.
- **Method Overriding:** To override a method in the derived class, the base class method must be abstract or virtual.

## Sealed Class

- **Definition:** A class that cannot have any child classes.

## Polymorphism

1. **Method Overriding:** Occurs between the base class and derived class with the same method signature (including access modifier, method name, and parameters) but different implementations.
2. **Method Overloading:** Occurs in the same class with the same method name and access modifiers but different input/output parameters.

## Static

- **Static Members:** Belong to the class itself instead of any instance.
- **Static Class:** All members should be static.

### Static Class vs Sealed Class

1. **Inheritance:**
   - Both cannot be inherited.
2. **Instance Creation:**
   - Cannot create an instance of a static class.
   - Can create an instance of a sealed class.
3. **Methods:**
   - Sealed class can contain both static and non-static methods.
   - Static class can contain only static methods.

### Abstract Class vs Static Class

1. **Instance Creation:**
   - Both cannot be instantiated.
2. **Inheritance:**
   - Abstract class should be inherited.
   - Static class cannot be inherited.
3. **Methods:**
   - Abstract class can contain both static and non-static methods.
   - Static class can contain only static methods.

### Use Cases of Static Class

1. Provide utilities.
2. Extension methods.
3. Configuration (e.g., database configuration class: db name, port number, connection string, etc.).
4. Design patterns (e.g., singleton design pattern).

## Extension Methods

- **Definition:** Allows adding additional functionalities to an existing type without modifying, deriving, or recompiling the original class.

### Syntax

1. The class must be a static class.
2. The method should be a static method.
3. The first parameter of the extension method must be of the type being extended.
4. The first parameter should be preceded by the `this` keyword.

```csharp
namespace ExtensionMethods
{
    public static class MyExtensions
    {
        public static int WordCount(this string str)
        {
            return str.Split(new char[] { ' ', '.', '?' },
                             StringSplitOptions.RemoveEmptyEntries).Length;
        }
    }
}
```

## SOLID Principles

- **O:** Open/Closed Principle - Objects/entities should be open for extension but closed for modification.

## LINQ

- **Definition:** Language Integrated Query; built-in extension methods.

## Casing Techniques

1. **Pascal Casing:** The first letter of an identifier must be uppercase, and the remaining letters must be lowercase. Used for naming classes, methods, namespaces, interfaces, delegates, and properties.
   - Example: `ExtensionMethodDemo.cs`, `ConsoleApp`.
2. **Camel Casing:** The first word is all lowercase, and subsequent words follow Pascal casing. Used for naming variables, objects, etc.
   - Example: `camelCaseExample`.

# C# Advanced Topics

## Reasons Object Type is Not Suitable for Passing Parameters
1. **Lack of Type Safety:** Using the `object` type does not provide compile-time type checking, which can lead to runtime errors.
2. **Unwanted Boxing:** Passing value types as objects causes boxing, which can degrade performance.

## Generics
- **Definition:** Generics allow us to define classes and methods while deferring the specification of types until the classes or methods are declared or called.

### Use Cases of Generics
- **Interfaces:** Used to include all common behaviors.

## Interfaces
1. **Definition:** A collection of methods that are by default abstract and public, to be implemented by derived classes.
2. **Multiple Implementations:** One class can implement multiple interfaces.
3. **Instantiation:** Interfaces cannot be instantiated.
4. **Loose Coupling:** Interfaces help in writing loosely coupled code.

### Abstract Class vs. Interface (Abstraction)
1. **Abstract Class:** Provides a base class to its subclasses and is a wise choice when we have a class hierarchy. It can contain both abstract and non-abstract methods.
2. **Interface:** Defines common functionalities and behaviors that can be implemented by any class. All methods are public and abstract by default.
3. **Inheritance:**
   - A class can inherit only one abstract or concrete class.
   - A class can implement multiple interfaces.

### Example:
```csharp
public interface IRepository {
    void Create();
    List<T> GetAll();
    T GetById(int id);
    void Update(T entity);
    void Delete(int id);
}

public interface ICustomerRepository {
    Customer GetCustomerByEmail(string email);
    List<Customer> GetCustomerByCity(string city);
}

public interface IProductRepository {
    Product GetProductByCategory(string category);
}

public class CustomerRepository : IRepository, ICustomerRepository {
    // Implementation of methods
}

public class ProductRepository : IRepository, IProductRepository {
    // Implementation of methods
}
```

## SOLID Principles

### Single Responsibility Principle (SRP)
- A class should have only one reason to change; it should be responsible for only one thing.

### Open/Closed Principle (OCP)
- Software entities like classes, modules, functions, etc., should be open for extension but closed for modification.
- **Implementation:** Use extension methods or inheritance.

### Liskov Substitution Principle (LSP)
- Derived classes should be substitutable for their base types.

### Interface Segregation Principle (ISP)
- Clients should not be forced to depend on interfaces they do not use.
- **Implementation:**
```csharp
public interface IRepository {
    void Create();
    List<T> GetAll();
    T GetById(int id);
    void Update(T entity);
    void Delete(int id);
}

public interface ICustomerRepository {
    Customer GetCustomerByEmail(string email);
}

public interface IProductRepository {
    Product GetProductByCategory(string category);
}
```

### Dependency Inversion Principle (DIP)
- High-level modules should not depend on low-level modules; instead, both should depend on abstractions.
- **Implementation:** Use dependency injection to achieve loosely coupled code.

## Collections

### Generic vs. Non-Generic Collections
1. **Non-Generic Collection:** Takes the `object` type, allowing a collection to contain different types of elements (both value and reference types). This can lead to unwanted boxing.
2. **Generic Collection:** Specifies the type, providing type safety and better performance.

### Advantages of Generic Collections
1. **Type Safety:** Compile-time type checking prevents runtime errors.
2. **Better Performance:** Avoids boxing/unboxing overhead.
3. **Flexibility:** Can define collections of any type.
4. **Maintainability:** Easier to read and maintain type-specific code.

### Example:
```csharp
List<int> numbers = new List<int>(); // Generic collection
numbers.Add(1);
numbers.Add(2);

ArrayList numbers = new ArrayList(); // Non-generic collection
numbers.Add(1);
numbers.Add("two"); // Lack of type safety
```

## Delegates

- **Definition:** A delegate is a type-safe function pointer that takes a function or method as a parameter. Delegates are reference types.

### Built-in Delegates

1. **Action:** Takes a function with generic input but returns void.
2. **Predicate:** Takes a function with generic input and returns a boolean value.
3. **Func:** Takes a function with generic input and returns a generic output.

### Example:

csharp

Copy code

`Action<string> print = Console.WriteLine; Predicate<int> isPositive = x => x > 0; Func<int, int, int> add = (a, b) => a + b;`

## Anonymous Methods and Types

- **Anonymous Method:** A method without a name, allowing creation of methods on the fly.
- **Anonymous Type:** Encapsulates a set of read-only properties into a single object without explicitly defining a type, created using the `new` keyword. They are reference types.

### Example:
```csharp
var anonymousType = new { Name = "John", Age = 30 }; Console.WriteLine(anonymousType.Name);
```

## `var` Keyword

- Used to declare a variable without assigning an explicit type.

### Example:
```csharp
var number = 10; // Implicitly typed as int
var name = "John";// Implicitly typed as string
```

## Exception Handling

- **Definition:** Runtime errors that can be caught using `try`, `catch`, and `finally` blocks.

### System.Exception Class Hierarchy

- **SystemException Class:**
    - **OutOfMemoryException**
    - **StackOverflowException**
    - **ArgumentException:**
        - **ArgumentNullException**
        - **ArgumentOutOfRangeException**
    - **ArithmeticException:**
        - **DivideByZeroException**
        - **OverflowException**

### Custom Exception Class

- Custom exception classes inherit from the `System.Exception` base class.

### Example:
```csharp
public class CustomException : Exception
{
	public CustomException(string message) : base(message)
	{
		
	}
}
```

## Finally Block

- Ensures execution regardless of an exception being thrown or not.

### Use Cases:

1. **Call `Dispose()` Method:** To clean up unmanaged resources from the unmanaged heap.
2. **Rollback Transactions:** Ensure database transactions are properly handled.

### Example:
```csharp
try {
    // Start a transaction
    // Commit transaction
} catch (Exception ex) {
    // Handle exception
} finally {
    if (transaction != null) {
        // Rollback transaction
    }
}
```

### LINQ: Language Integrated Query
LINQ is a SQL-like syntax that helps us query different data sources. It includes various query expressions on the `IEnumerable<T>` interface.

#### Types of LINQ:
1. **LINQ to Objects**: 
    - Allows querying in-memory data sources like lists, arrays, or collections.
    - The return type is `IEnumerable`, the base interface for all collections and interfaces.
2. **LINQ to Datasets**: 
    - Allows working with ADO.Net.
3. **LINQ to SQL**: 
    - Allows querying SQL Server databases.
    - The return type is `IQueryable`.
4. **LINQ to Entities**: 
    - Allows querying other SQL databases or entity frameworks.
    - The return type is `IQueryable`.

#### In-Memory vs. Out-of-Memory Data Sources:
- **In-Memory Data Sources**: `IEnumerable`
- **Out-of-Memory Data Sources**: `IQueryable`

### Returning a Single Record:
1. **First**:
    - Returns the very first record when one or more matching values are found.
    - Throws an exception if no matching record is found.
2. **FirstOrDefault**:
    - Returns the very first record when one or more matching values are found.
    - Returns a default value (null if not specified) if no matching record is found.
3. **Single**:
    - Returns the only matched record.
    - Throws an exception if no matching record is found or if more than one matching record is found.
4. **SingleOrDefault**:
    - Returns the only matched record.
    - Returns a default value (null if not specified) if no matching record is found.
    - Throws an exception if more than one matching record is found.

### Quantifier Operators:
1. **Any()**:
    - Checks if any elements satisfy the specified condition.
    - Returns `true` if any elements satisfy the condition; otherwise returns `false`.
2. **All()**:
    - Checks if all elements satisfy the specified condition.
    - Returns `true` if all elements satisfy the condition; otherwise returns `false`.

### Execution Types:
- **Deferred Execution**: LINQ queries are not executed until the query is iterated over.
- **Immediate Execution**: Methods like `ToList()` and `ToArray()` force immediate execution of a query.

### Joins:
1. **Inner Join**:
    ```csharp
    var result = from c in Customers 
                 join o in Orders on c.CustomerID equals o.CustomerID
                 select new { c.CustomerID, c.ContactName, o.OrderDate };
    ```
2. **Left Join**:
    ```csharp
    var result = from c in Customers 
                 join o in Orders on c.CustomerID equals o.CustomerID into customerOrders
                 from co in customerOrders.DefaultIfEmpty()
                 select new { c.CustomerID, c.ContactName, co?.OrderDate };
    ```
