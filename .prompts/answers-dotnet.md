# Answers: .Net

## Contents
- `Entry`
    - [What are Property Accessors?](#entry-what-are-property-accessors)
    - [What is the difference between continue and break statements in C#?](#entry-what-is-the-difference-between-continue-and-break-statements-in-c)
- `Junior`
    - [What is enum in C#?](#junior-what-is-enum-in-c)
    - [Can multiple catch blocks be executed?](#junior-can-multiple-catch-blocks-be-executed)
- `Mid`
    - [When to use Record vs Class vs Struct in C#?](#mid-when-to-use-record-vs-class-vs-struct-in-c)
- `Senior`
    - [What is difference between late binding and early binding in C#?](#senior-what-is-difference-between-late-binding-and-early-binding-in-c)
- `Expert`
    - [Why doesn't C# allow static methods to implement an interface?](#expert-why-doesnt-c-allow-static-methods-to-implement-an-interface)
---

## `Entry` What are Property Accessors?
Property accessors in C# are special methods called "getters" and "setters" that allow controlled access to a class’s fields. The `get` accessor returns the property value, while the `set` accessor assigns a new value. These encapsulate the field, allowing validation, logging, or encapsulation logic. Auto-implemented properties can use default get/set without providing method bodies. Accessors can have different accessibilities (e.g., public get, private set), increasing flexibility and security. Properties are accessed like fields but are implemented with methods. This mechanism adheres to encapsulation in object-oriented programming by hiding data implementation details and exposing only required functionality. You can also define “read-only” (only get) or “write-only” (only set) properties.

```csharp
private int _age;
public int Age {
    get {
        return _age; 
    }
    set { 
        if (value > 0) 
            _age = value; 
    }
}
```
---

## `Entry` What is the difference between continue and break statements in C#?
The `break` statement is used to immediately exit a loop or switch statement, terminating the execution of the enclosing loop. Conversely, the `continue` statement skips the remaining statements in the current iteration and proceeds to the next iteration of the loop. `break` is generally used when a certain condition is met and no further iterations are needed, while `continue` is useful for bypassing specific conditions within a loop but not stopping the loop entirely. Both statements help control flow within loops, but they serve different purposes based on whether you want to halt or skip iterations.

```csharp
for (int i = 0; i < 5; i++) {
    if (i == 2) continue; // skips i=2
    if (i == 4) break;    // stops the loop at i=4
    Console.WriteLine(i);
}
```
---

## `Junior` What is enum in C#?
An enum (enumeration) in C# is a value type that consists of a set of named constants called members. Enums make code more readable and maintainable by assigning names to sets of numeric values, instead of using magic numbers. By default, the underlying type is `int`, but you can specify other integral types. Enums are commonly used to represent a fixed set of related constants, like days of the week, months, or status codes. They enhance code clarity, type safety, and reduce errors associated with invalid values.

```csharp
enum Day { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday }
Day today = Day.Monday;
```
---

## `Junior` Can multiple catch blocks be executed?
No, multiple catch blocks cannot be executed for a single exception in C#. When an exception occurs in a try block, the runtime searches for the first catch block that matches the exception type, executes it, and then exits the exception handling structure. Only one catch block runs per exception. Multiple catch blocks allow you to handle different exception types separately, but only one will be triggered for the thrown exception.

```csharp
try {
    // code that throws exception
} catch (FormatException ex) {
    // handles FormatException
} catch (Exception ex) {
    // handles all other exceptions
}
```
---

## `Mid` When to use Record vs Class vs Struct in C#?

Use a record when you want an immutable reference type primarily meant for data storage with value-based equality—commonly in scenarios like DTOs. Use a class for complex objects requiring reference semantics, mutable state, or encapsulating behavior. Structs are best for lightweight, immutable, value types that have short lifespans and don’t need inheritance—such as points, colors, or coordinates. Avoid using structs for large types because copying can be expensive. Record structs (introduced in C# 10) offer value-based equality for structs. Choose based on size, immutability, equality needs, and whether you need inheritance.

```csharp
// Record
public record Person(string Name, int Age);

// Class
public class Car { 
    public string Model; 
    public int Year; 
}

// Struct
public struct Point { 
    public int X, Y; 
}
```
---

## `Senior` What is difference between late binding and early binding in C#?
Early binding refers to compile-time linkage where the compiler knows the type and method to call. It offers better performance and compile-time checking. Late binding happens at runtime, where the exact type or method is determined dynamically. This is typically achieved using reflection or `dynamic` variables in C#. Late binding is more flexible but slower and error-prone because type checking is deferred to runtime. Use early binding for performance and safety; use late binding where flexibility is needed, e.g., when working with COM objects or plugins.
```csharp
// Early binding
MyClass obj = new MyClass();
obj.Method();

// Late binding
object obj = Activator.CreateInstance(type);
MethodInfo method = type.GetMethod("Method");
method.Invoke(obj, null);
```
---

## `Expert` Why doesn't C# allow static methods to implement an interface?

C# does not allow static methods to implement an interface because interfaces are contracts for instance behavior, not for static type-level behavior. When a class implements an interface, it provides object-level behavior—any interface method is meant to be called on an instance of that class. Static methods belong to the type itself and cannot be called on an instance, so they can’t fulfill interface contracts that operate through polymorphism (where you use instances via their interface references). Allowing static methods in interfaces would break this model, making code less predictable and weakening the principles of object-oriented design such as polymorphism and inheritance. Additionally, interfaces are about substitutability—one instance for another—something static methods cannot participate in, since they do not use or refer to any particular object. Starting with C# 8, interfaces can provide static members with default implementations, but they still cannot be made abstract or enforced by implementing classes.

```csharp
interface IExample
{
    void DoWork(); // Allowed
    // static void StaticMethod(); // Not allowed
}

class Worker : IExample
{
    public void DoWork() { /* ... */ }
    public static void StaticMethod() { /* ... */ } // Not related to interface
}
```
---