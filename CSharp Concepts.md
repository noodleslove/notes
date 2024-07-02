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