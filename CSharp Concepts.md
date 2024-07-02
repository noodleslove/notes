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

