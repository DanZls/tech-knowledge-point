# Entry

## Q1: What are Property Accessors?
Property accessors in C# are special methods called "getters" and "setters" that allow controlled access to a class’s fields. The `get` accessor returns the property value, while the `set` accessor assigns a new value. These encapsulate the field, allowing validation, logging, or encapsulation logic. Auto-implemented properties can use default get/set without providing method bodies. Accessors can have different accessibilities (e.g., public get, private set), increasing flexibility and security. Properties are accessed like fields but are implemented with methods. This mechanism adheres to encapsulation in object-oriented programming by hiding data implementation details and exposing only required functionality. You can also define “read-only” (only get) or “write-only” (only set) properties.

```csharp
private int _age;
public int Age {
    get { return _age; }
    set { if (value > 0) _age = value; }
}
```
---

## Q2: What is the difference between continue and break statements in C#?
The `break` statement is used to immediately exit a loop or switch statement, terminating the execution of the enclosing loop. Conversely, the `continue` statement skips the remaining statements in the current iteration and proceeds to the next iteration of the loop. `break` is generally used when a certain condition is met and no further iterations are needed, while `continue` is useful for bypassing specific conditions within a loop but not stopping the loop entirely. Both statements help control flow within loops, but they serve different purposes based on whether you want to halt or skip iterations.

```csharp
for (int i = 0; i < 5; i++) {
    if (i == 2) continue; // skips i=2
    if (i == 4) break;    // stops the loop at i=4
    Console.WriteLine(i);
}
```
---

## Q3: What is C#?
C# is a modern, type-safe, object-oriented programming language developed by Microsoft as a part of the .NET platform. It is designed for building a wide range of applications, including web, desktop, cloud, and mobile. C# supports strong type checking, object-oriented principles (inheritance, encapsulation, and polymorphism), and component-oriented and functional programming paradigms. It features automatic garbage collection, rich standard libraries, and support for modern language constructs like LINQ, async/await, lambda expressions, and events. C# syntax is similar to other C-family languages and is recognized for its readability and productivity enhancements. Applications written in C# are compiled to Intermediate Language (IL), allowing cross-platform deployment via .NET.

```csharp
using System;
class Program {
    static void Main() {
        Console.WriteLine("Hello, World!");
    }
}
```
---

## Q4: What is an Object?
An object in C# is an instance of a class, encapsulating data (fields/properties) and behavior (methods). Objects are created from class blueprints, allowing multiple instances with unique states. Each object has its own identity, state, and behavior. Objects support encapsulation, inheritance, and polymorphism, making them the building blocks of object-oriented programming. Objects interact with each other through methods and can represent physical, conceptual, or logical entities. They provide abstraction, allowing code reuse and modularity in software development.

```csharp
class Car {
    public string Model { get; set; }
}
Car myCar = new Car();
myCar.Model = "Toyota";
```
---

## Q5: What are partial classes?
Partial classes in C# allow a single class to be split across multiple files. Each part must use the `partial` keyword and, when compiled, all parts are combined into one class. This feature is useful in large projects, code generation scenarios (such as designer files in Windows Forms), and for separating automatically generated code from user code. It enhances collaboration, code organization, and maintainability. All parts of a partial class must reside in the same namespace and assembly. Partial classes can contain fields, properties, methods, events, etc., and access modifiers must be consistent.

```csharp
// File1.cs
public partial class Person {
    public string Name { get; set; }
}
// File2.cs
public partial class Person {
    public void SayHello() {
        Console.WriteLine($"Hello, {Name}");
    }
}
```
---

# Junior

## Q6: What is enum in C#?
An enum (enumeration) in C# is a value type that consists of a set of named constants called members. Enums make code more readable and maintainable by assigning names to sets of numeric values, instead of using magic numbers. By default, the underlying type is `int`, but you can specify other integral types. Enums are commonly used to represent a fixed set of related constants, like days of the week, months, or status codes. They enhance code clarity, type safety, and reduce errors associated with invalid values.

```csharp
enum Day { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday }
Day today = Day.Monday;
```
---

## Q7: Can multiple catch blocks be executed?
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

## Q8: What is namespace in C#?
A namespace in C# is a logical container for types such as classes, interfaces, enums, and structs. Namespaces organize code, prevent naming conflicts, and enable logical grouping of related code elements. They allow you to define identical type names within different namespaces without collision. Namespaces also help manage large codebases and provide scope to identifiers. You use the `using` directive to reference namespaces in your code.

```csharp
namespace Project.Library {
    class Helper { }
}
// Usage
using Project.Library;
Helper h = new Helper();
```
---

## Q9: How is Exception Handling implemented in C#?
Exception handling in C# is performed using the `try`, `catch`, `finally`, and `throw` keywords. The `try` block contains code that may throw exceptions. When an exception occurs, control is passed to the appropriate `catch` block. You can define multiple catch blocks to handle specific or general exceptions. The `finally` block, if present, executes regardless of whether an exception was thrown and is typically used for cleanup. Exceptions can be thrown manually using the `throw` statement.

```csharp
try {
    int a = int.Parse("abc");
} catch (FormatException ex) {
    Console.WriteLine("Format error");
} finally {
    Console.WriteLine("Done");
}
```
---

## Q10: What is the difference between string and StringBuilder in C#?
A `string` in C# is an immutable object, meaning its value cannot change after creation. Any modification (concatenation, replacement) creates a new string object. This can lead to memory overhead when many string modifications occur. `StringBuilder` is a mutable class designed for efficient string manipulation, especially when repeatedly modifying or appending strings. `StringBuilder` reduces the number of intermediate objects and improves performance in scenarios with extensive string changes.

```csharp
string s = "Hello";
s += " World"; // Creates a new string
StringBuilder sb = new StringBuilder("Hello");
sb.Append(" World"); // Modifies the same object
```
---

## Q11: What is Boxing and Unboxing?
Boxing is the process of converting a value type (such as int) to a reference type (object), allowing it to be treated as an object. Unboxing is the reverse: extracting the value type from the object. Boxing involves copying the value type to the heap and wrapping it in an object. Unboxing requires explicit casting and retrieves the value type from the object. Boxing and unboxing can introduce performance overhead, so they should be used carefully.

```csharp
int x = 10;
object obj = x;          // Boxing
int y = (int)obj;        // Unboxing
```
---

## Q12: What is LINQ in C#?
LINQ (Language Integrated Query) is a feature in C# that enables querying collections in a syntax similar to SQL, directly within the language. It provides a consistent query experience for collections, databases, XML, and other data sources. LINQ enhances code readability and reusability, supports filtering, ordering, grouping, projection, and aggregation operations, and can be used with both query syntax and method syntax.

```csharp
int[] numbers = { 1, 2, 3, 4 };
var even = from n in numbers where n % 2 == 0 select n;
```
---

## Q13: What is Serialization?
Serialization is the process of converting an object into a format (like JSON, XML, or binary) that can be stored or transmitted and later reconstructed (deserialized). Serialization is widely used for data persistence, deep copying, or communication between applications and services. C# provides serialization support through libraries like System.Text.Json, Newtonsoft.Json, and XML serialization. Objects to be serialized should be marked as `[Serializable]` (for binary/XML) or use data contract attributes as per requirement.

```csharp
[Serializable]
public class Person {
    public string Name { get; set; }
}
// Serialization example with JSON
// string json = JsonSerializer.Serialize(person);
```
---

## Q14: What are dynamic type variables in C#?
Dynamic type variables, declared with the `dynamic` keyword, can store any type and their type is resolved at runtime instead of compile time. This allows late binding and bypasses compile-time type checking, enabling scenarios like interop with COM objects, dynamic languages, or reflection. However, misuse can lead to runtime errors if members or methods don't exist. They provide flexibility at the cost of type safety.

```csharp
dynamic val = 10;
val = "Hello"; // type can change at runtime
Console.WriteLine(val.Length); // valid for string
```
---

## Q15: What are the different types of classes in C#?
C# provides several types of classes:
- **Normal (Concrete) classes**: Can be instantiated and may have fields, properties, methods.
- **Abstract classes**: Cannot be instantiated directly, and may contain abstract members.
- **Static classes**: Cannot be instantiated, only contain static members.
- **Partial classes**: Split definitions across multiple files.
- **Sealed classes**: Cannot be inherited.
Each type serves different design needs, such as enforcing inheritance, utility methods, or code organization.

```csharp
abstract class Shape { }
static class Utils { }
sealed class SingleUse { }
partial class Account { }
```
---

## Q16: What is the difference between a Struct and a Class in C#?
Structs are value types and are stored on the stack, whereas classes are reference types stored on the heap. Structs cannot inherit from other structs or classes, but they can implement interfaces. Structs do not support inheritance but can have constructors, fields, methods, and properties. Classes can have destructors, support inheritance, and are more suitable for complex data and behaviors. Structs are typically used for small, simple objects.

```csharp
struct Point { public int X, Y; }
class Person { public string Name; }
```
---

## Q17: In how many ways you can pass parameters to a method?
C# allows parameters to be passed to methods in these ways:
- **By value** (default): method receives a copy of the variable.
- **By reference** (`ref`): method can modify the original variable.
- **As output** (`out`): method returns a value via parameter (must be assigned inside the method).
- **As parameter array** (`params`): allows variable number of arguments.

```csharp
void Foo(int x) {}
void Bar(ref int x) {}
void Baz(out int x) { x = 5; }
void Qux(params int[] numbers) {}
```
---

## Q18: Can this be used within a Static method?
No, the `this` keyword cannot be used within a static method because `this` refers to the current instance of a class, while static methods are called on the class itself (not on an instance). Static methods cannot access instance members or properties; they can only access static members.

```csharp
static void MyStaticMethod() {
    // this.SomeInstanceMethod(); // Error
}
```
---

## Q19: Why to use finally block in C#?
The `finally` block is used to execute code regardless of whether an exception occurs or not. Typically, it's used for cleanup activities such as closing files, releasing resources, or disconnecting from databases, ensuring critical code always runs. It runs after try and catch blocks have executed and is optional.

```csharp
try {
    // risky operation
} catch {
    // handle exception
} finally {
    // cleanup code, always runs
}
```
---

## Q20: What are Nullable types in C#?
Nullable types allow value types (like int, float, etc.) to represent null values. This is useful when dealing with databases or data where a value may be undefined. Nullable types are defined using `?` (e.g., int?). Use the `HasValue` property to check if a value exists; access the value via the `Value` property.

```csharp
int? age = null;
if (age.HasValue) {
    Console.WriteLine(age.Value);
}
```
---

## Q21: What is Managed or Unmanaged Code?

Managed code is code that is executed by the .NET Common Language Runtime (CLR), which provides services such as garbage collection, type safety, exception handling, and security. The CLR manages the execution of this code, ensuring better memory management and system stability. Unmanaged code, on the other hand, is executed directly by the operating system outside of the CLR. Examples of unmanaged code include code written in languages like C or C++ or when using COM components or system APIs. Unmanaged code does not benefit from the services provided by CLR, making developers responsible for memory management and avoiding memory leaks. In .NET, it’s common to interact with unmanaged code using Platform Invocation Services (P/Invoke) or COM Interop when necessary. Using unmanaged code can be necessary for performance reasons or when accessing low-level system resources, but it also increases risks related to security and memory leaks compared to managed code.

```csharp
// Managed code example:
public class ManagedSample {
    public void ShowMessage() {
        Console.WriteLine("This is managed code.");
    }
}

// Unmanaged code interop example:
[DllImport("user32.dll")]
public static extern int MessageBox(IntPtr hWnd, string text, string caption, uint type);
```
---

## Q22: What is the difference between a class and a structure?

In C#, classes and structures are both used to define custom types, but they differ significantly. Classes are reference types stored on the heap, while structures are value types stored on the stack. Classes support inheritance, destructors, and can have parameterless constructors, while structures cannot inherit from another class or struct, nor have destructors or explicit parameterless constructors. Structures are best used for small data-centric types, while classes offer more sophistication and object-oriented features. Structs are copied by value, meaning changes to a copied struct do not affect the original, while classes are copied by reference. Structs implicitly derive from System.ValueType, whereas classes derive from System.Object. Memory management and performance characteristics are key differentiators when choosing between them.

```csharp
// Class example
public class Person {
    public string Name;
}

// Struct example
public struct Point {
    public int X, Y;
}
```
---

## Q23: What do you understand by Value types and Reference types in .NET? Provide some comparison.

Value types directly contain their data and are typically stored on the stack. Examples include int, struct, and enum. When assigned or passed to methods, value types are copied, making them independent instances. Reference types, like classes, arrays, and delegates, store references to the actual data, which resides on the heap. When assigned, reference types only copy the reference, not the actual data, meaning changes to one reference affect all references pointing to that object. Value types cannot be null (unless they are nullable), whereas reference types can. Value types offer performance benefits for small objects, but reference types are preferred for complex, large objects with behaviors.

```csharp
// Value type example
int a = 10;
int b = a; // b is a copy

// Reference type example
class Demo { public int Value; }
Demo obj1 = new Demo();
Demo obj2 = obj1; // obj2 references the same object as obj1
```
---

## Q24: What are Reference Types in C#?

Reference types are types where the variable holds a reference to the data’s memory location rather than containing the data directly. Examples include classes, interfaces, delegates, arrays, and strings. When a reference type variable is assigned to another, both point to the same memory location; modifying one affects the other. Reference types are allocated on the managed heap, and their lifecycle is managed by the .NET garbage collector. They allow for more complex structures, dynamic memory usage, and polymorphic behavior, especially important in object-oriented programming.

```csharp
// Reference type example
class Car { public string Model; }
Car c1 = new Car { Model = "Sedan" };
Car c2 = c1;
c2.Model = "SUV"; // c1.Model is now "SUV" due to referencing the same object
```
---

## Q25: What is an Abstract Class?

An abstract class in C# is a class that cannot be instantiated directly and may contain abstract methods (methods without implementation) as well as fully implemented methods. It serves as a base for other classes, enforcing that certain members must be implemented in derived classes. Abstract classes can contain fields, properties, and methods, and support constructors. They are used when you want to provide some common functionality, but also want to force derived classes to implement specific behaviors. Abstract classes enable partial code reuse and the enforcement of a contract for subclasses.

```csharp
public abstract class Animal {
    public abstract void Speak();
    public void Eat() { Console.WriteLine("Eating..."); }
}

public class Dog : Animal {
    public override void Speak() { Console.WriteLine("Bark"); }
}
```
---

## Q26: What are generics in C#?

Generics allow you to design classes, interfaces, methods, and delegates with a placeholder for the data type, promoting code reuse and type safety. By using generics, you avoid code duplication and runtime type errors because the type is checked at compile time. The .NET Framework provides generic collections like List<T> and Dictionary<TKey, TValue>. Generics increase performance by eliminating the need for boxing/unboxing and casting, and they help create reusable, well-typed code usable across various data types.

```csharp
// Generic class example
public class Box<T> {
    public T Content;
}

// Usage:
Box<int> intBox = new Box<int> { Content = 42 };
Box<string> strBox = new Box<string> { Content = "Hello" };
```
---

# Mid

## Q27: When to use Record vs Class vs Struct in C#?

Use a record when you want an immutable reference type primarily meant for data storage with value-based equality—commonly in scenarios like DTOs. Use a class for complex objects requiring reference semantics, mutable state, or encapsulating behavior. Structs are best for lightweight, immutable, value types that have short lifespans and don’t need inheritance—such as points, colors, or coordinates. Avoid using structs for large types because copying can be expensive. Record structs (introduced in C# 10) offer value-based equality for structs. Choose based on size, immutability, equality needs, and whether you need inheritance.

```csharp
// Record
public record Person(string Name, int Age);

// Class
public class Car { public string Model; public int Year; }

// Struct
public struct Point { public int X, Y; }
```
---

## Q28: What is Record in C#?

A record in C# is a reference type introduced in C# 9, designed for immutable data models and value-based equality. When two record objects have the same data, they are considered equal, which differs from classes that default to reference equality. Records support concise syntax with positional parameters and allow inheritance. Records are especially useful for DTOs, modeling data, and functional programming scenarios. They also provide built-in support for "with-expressions" to create modified copies.

```csharp
public record Person(string Name, int Age);

var p1 = new Person("Alice", 30);
var p2 = p1 with { Age = 31 };
```
---

## Q29: What are the uses of 'using' in C#?

The 'using' keyword in C# has two main purposes. First, as a directive, it imports namespaces to avoid fully qualified type names. Second, as a statement, it ensures proper resource management by automatically disposing of IDisposable objects at the end of the block, preventing resource leaks with files, streams, or database connections. The 'using' statement supports both old (braces) and modern (declaration-only) syntax.

```csharp
// Namespace import
using System.IO;

// Resource management
using (var file = File.Open("test.txt", FileMode.Open)) {
    // file operations
}
```
---

## Q30: Explain the difference between Task and Thread in .NET

A Thread represents an independent path of execution in an application and is managed directly by the programmer. Tasks, introduced with TPL, are abstractions over threads used primarily for asynchronous and parallel programming. Tasks are more lightweight, managed by the task scheduler, and can use thread pool threads. Tasks provide better resource management, support for continuations, and easier exception handling. Threads are appropriate for low-level threading control while Tasks suit higher-level asynchronous operations.

```csharp
// Thread
Thread t = new Thread(() => Console.WriteLine("Hello, Thread!"));
t.Start();

// Task
Task.Run(() => Console.WriteLine("Hello, Task!"));
```
---

## Q31: What is the use of the IDisposable interface?

The IDisposable interface provides the Dispose() method to release unmanaged resources like files, database connections, or network streams deterministically. Implementing IDisposable allows objects to be used within a 'using' block, ensuring resources are cleaned up even if exceptions occur. It is especially important for objects using resources not managed by the .NET runtime (like file handles or GDI+ objects). Classes with unmanaged resources must implement IDisposable to avoid resource leaks.

```csharp
public class FileManager : IDisposable {
    private FileStream stream;
    public void Dispose() { stream?.Dispose(); }
}
```
---

## Q32: Is there a way to catch multiple exceptions at once and without code duplication?

Yes, in C# 6 and later, you can use multiple exception types in a single catch block using filter expressions (catch when). Alternatively, you can catch the base Exception and inspect its type, though specific catch blocks for each exception type are clearer. This reduces code duplication by sharing the error handling logic rather than repeating it.

```csharp
try {
    // code
}
catch (IOException ex) when (ex is FileNotFoundException || ex is DirectoryNotFoundException) {
    Console.WriteLine("File or directory not found.");
}
```
---

## Q33: How is encapsulation implemented in C#?

Encapsulation is implemented by restricting access to the internals of a class, exposing only what is necessary through public members. Fields are typically marked private or protected, with public properties or methods controlling their access. This hides implementation details, provides validation, improves security, and makes code easier to maintain.

```csharp
public class Account {
    private decimal balance;

    public decimal Balance {
        get { return balance; }
        private set { balance = value; }
    }

    public void Deposit(decimal amount) {
        if (amount > 0) balance += amount;
    }
}
```
---

## Q34: Explain assignment vs shallow copy vs deep copy for a Record in C#

Assignment copies the reference, so both variables point to the same record instance. Shallow copy creates a new record object, but any reference-type fields inside still refer to the same objects. In records, 'with' expressions produce a shallow copy. Deep copy means cloning the object and all objects referenced by it, resulting in a completely independent object graph. You have to implement deep copy yourself (e.g., via serialization).

```csharp
public record Person(string Name, Address Addr);
public record Address(string Street);

// Assignment
Person p1 = new("Alice", new Address("Rd"));
Person p2 = p1; // same reference

// Shallow copy (with-expression)
Person p3 = p1 with { Name = "Bob" }; // Addr still the same

// Deep copy (manual, not automatic)
Person p4 = new(p1.Name, new Address(p1.Addr.Street));
```
---

## Q35: What is sealed Class in C#?

A sealed class cannot be inherited. Marking a class as sealed prevents other classes from deriving from it, which can improve performance (e.g., allow certain runtime optimizations) and is useful for API design when you want to prevent extension via inheritance for design reasons. Value types (structs) are implicitly sealed.

```csharp
public sealed class Logger {
    public void Log(string message) { /* ... */ }
}

// This will not work:
// public class MyLogger : Logger { }
```
---

## Q36: How can you prevent a class from being overridden in C#?

In C#, you prevent a class from being overridden by marking it as sealed. To prevent individual methods or properties from being overridden, you mark them as sealed when overriding a base virtual member in a derived class. This restricts further derived classes from changing that behavior.

```csharp
public sealed class FinalClass { }

// Sealed method example
public class Base {
    public virtual void Foo() { }
}
public class Derived : Base {
    public sealed override void Foo() { }
}
```
---

## Q37: Explain Code Compilation in C#

Code compilation in C# involves several steps. First, the source code (.cs files) is compiled by the C# compiler (csc.exe) into intermediate language (IL or MSIL), producing an assembly (.exe or .dll). This assembly contains IL code and metadata about types, members, and references. During execution, the .NET runtime's Just-In-Time (JIT) compiler converts IL into native machine code for the platform. This two-phase model enables cross-platform support and runtime optimizations. The process ensures type safety, security, and platform independence.

```csharp
// Code compilation steps
// 1. csc.exe compiles .cs -> .dll/.exe (IL code)
// 2. JIT compiles IL -> native machine code at runtime
```
---

## Q38: What is Extension Method in C# and how to use them?

An extension method allows you to "add" methods to existing types without modifying their source code or using inheritance. These are defined as static methods in static classes but are called as if they are instance methods on the extended type. The first parameter specifies 'this' followed by the type being extended. Extension methods are used to extend built-in types, add utility functions, and enhance existing APIs.

```csharp
public static class StringExtensions {
    public static bool IsNullOrEmpty(this string str) {
        return string.IsNullOrEmpty(str);
    }
}

// Usage
string name = "";
bool result = name.IsNullOrEmpty();
```
---

## Q39: What is an anonymous function in C#?

An anonymous function is a method without a name, defined inline using either lambda expressions or delegate syntax. They are often used as arguments for methods requiring a delegate, such as LINQ queries, event handlers, or asynchronous operations. Anonymous functions can capture variables from their enclosing scope, enabling flexible and powerful inline behavior.

```csharp
// Lambda expression (anonymous function)
Func<int, int, int> add = (a, b) => a + b;

// Delegate syntax
Func<int, int, int> multiply = delegate (int x, int y) { return x * y; };
```
---

## Q40: What is difference between constant and readonly?

A constant (const) is a compile-time constant, its value must be assigned at declaration and cannot change. It is implicitly static and can only be of primitive or string types. A readonly field can be assigned at declaration or in a constructor, allowing a value to be computed at runtime. Readonly fields are not implicitly static (but can be static), and their value can differ per instance. Use const for values known at compile-time and readonly for values set at runtime or per instance.

```csharp
public class Example {
    public const double Pi = 3.14159;        // Compile-time constant
    public readonly int Id;                  // Can be set in constructor

    public Example(int id) {
        Id = id;
    }
}
```
---

## Q41: What is Reflection in C#.Net?
Reflection in C# is the ability of a program to examine and interact with its own metadata, types, and objects at runtime. It allows you to inspect assemblies, modules, types, methods, properties, and fields dynamically. With reflection, you can create instances, invoke methods, and access fields or properties without knowing their names at compile time. This is especially useful in scenarios like creating plug-ins, object serialization, late binding, or working with attributes. However, reflection is slower than direct code access because it requires type discovery and is generally avoided in performance-critical code. Reflection is provided by the System.Reflection namespace. Security considerations should be taken into account, as reflection can access private members if permissions allow. Common uses include dynamic loading of assemblies, runtime type inspection, and building generic frameworks.
```csharp
// Example: Using reflection to get all property names of a class
Type type = typeof(DateTime);
foreach (var prop in type.GetProperties())
{
    Console.WriteLine(prop.Name);
}
```
---

## Q42: What is scope of a Internal member variable of a C# class?
An internal member variable in C# is accessible anywhere within the same assembly where it is declared but not from another assembly. The `internal` access modifier means the member is visible to all code in the same project (.exe or .dll), but hidden from other assemblies even if they reference it. This is useful for encapsulation, ensuring that implementation details are not exposed outside the assembly boundary. Internal members are often used for utility functions, helper classes, or data that should not be part of the public API. If tighter access is required, combine `internal` with `protected` to allow access only to derived types within the same assembly.
```csharp
public class MyClass
{
    internal int myVar; // Accessible within the same assembly ONLY
}
```
---

## Q43: What is the difference between overloading and overriding?
Overloading refers to defining multiple methods with the same name but different signatures (parameter lists) within the same class or scope. It is determined at compile-time (static polymorphism) and allows methods to perform similar but slightly different tasks depending on parameters. Overriding, on the other hand, occurs in derived classes where a method in the base class is redefined using the `override` keyword to alter or extend its behavior. Overriding requires inheritance, and the base method should be marked `virtual`, `abstract`, or `override`. Overriding is resolved at runtime (dynamic polymorphism), enabling runtime method binding.
```csharp
// Overloading
void Print(int i) { }
void Print(string s) { }

// Overriding
public class Base
{
    public virtual void Display() { Console.WriteLine("Base"); }
}
public class Derived : Base
{
    public override void Display() { Console.WriteLine("Derived"); }
}
```
---

## Q44: What is a Destructor in C# and when shall I create one?
A destructor in C# is a special method invoked when an object is garbage collected, used to release unmanaged resources before the object is destroyed. Unlike constructors, destructors cannot be called explicitly; they are invoked by the runtime garbage collector. You declare a destructor using a tilde (~) followed by the class name. Destructors are rare in modern C# due to the garbage collector, but are used when you deal with unmanaged resources like file handles, database connections, or pointers. It is generally recommended to implement the `IDisposable` interface for resource cleanup instead of relying solely on destructors.
```csharp
class MyClass
{
    ~MyClass()
    {
        // Cleanup code here
    }
}
```
---

## Q45: What is the difference between Interface and Abstract Class?
Interfaces define a contract: a set of methods and properties that implementing types must provide, but do not contain any implementation (until C# 8, which allows default interface methods). Abstract classes can have both abstract members (without implementation) and concrete members (with implementation). A class can implement multiple interfaces but can inherit from only one abstract class (C# supports single inheritance for classes). Interfaces are used for loosely coupled architectures, while abstract classes are for sharing a common base with partial implementations.
```csharp
interface IAnimal
{
    void Speak();
}

abstract class Animal
{
    public abstract void Speak();
    public void Eat() { Console.WriteLine("Eat"); }
}
```
---

## Q46: Is there a difference between throw and throw ex?
Yes, there is a significant difference. Using `throw` in a catch block re-throws the original exception, preserving the original call stack, which is important for debugging. Using `throw ex` creates a new exception and resets the stack trace to the line where `throw ex` is called, making it harder to trace the source of the error. Best practice is to use `throw` to preserve this information unless you explicitly need to create a new exception.
```csharp
try
{
    // code
}
catch (Exception ex)
{
    throw; // preserves original stack trace
    // throw ex; // resets stack trace (not recommended)
}
```
---

## Q47: What is the difference between ref and out keywords?
Both `ref` and `out` are used to pass arguments by reference to methods. The key difference is that `ref` requires the variable to be initialized before passing it, while `out` does not. With `out`, the method must assign a value before the method returns. `ref` is used when the value coming in matters; `out` is used for methods returning multiple values through parameters.
```csharp
void TestRef(ref int x) { x += 5; }
void TestOut(out int y) { y = 10; }

int a = 1;
TestRef(ref a); // a is now 6

int b;
TestOut(out b); // b is now 10
```
---

## Q48: Explain Anonymous type in C#
Anonymous types in C# are simple objects created on the fly without explicitly declaring a class. They're commonly used with LINQ queries for creating data-shaped objects with specified properties. Anonymous types are immutable, have compiler-generated names, and are useful for temporary data grouping or projection. You can only use them within the same method since their type is not directly accessible outside.
```csharp
var person = new { Name = "Alice", Age = 25 };
Console.WriteLine(person.Name); // Output: Alice
```
---

## Q49: Why can't you specify the accessibility modifier for methods inside the Interface?
In C#, interface members are implicitly public, as interfaces define a public contract that all implementing types must provide. Specifying an access modifier is redundant and not allowed. The goal is to ensure uniform accessibility for all implementers, so interface methods cannot be private or protected; they describe the required public APIs.
```csharp
interface IExample
{
    void Display(); // Implicitly public, no modifier allowed
}
```
---

## Q50: What is the difference between dynamic type variables and object type variables?
Both `dynamic` and `object` variables can hold any type, but there's a key difference in how operations are resolved. Variables of type `object` require explicit casting to access specific members at compile time. With `dynamic`, all type checking is deferred to runtime, enabling member access without casting, but risking runtime exceptions if members do not exist. `dynamic` is useful for interoperability with COM or dynamic languages, while `object` is preferred for general-purpose scenarios where type safety is important.
```csharp
object obj = "hello";
string s1 = (string)obj; // requires casting

dynamic dyn = "world";
string s2 = dyn.ToUpper(); // no compile-time checking
```
---

## Q51: What is the difference between Virtual method and Abstract method?
A virtual method in a base class provides a default implementation and can be optionally overridden by derived classes using the `override` keyword. An abstract method has no implementation in the base class and must be overridden in any non-abstract derived class. Abstract methods can only exist inside abstract classes, while virtual methods can exist in both normal and abstract classes.
```csharp
abstract class Base
{
    public virtual void Foo() { Console.WriteLine("Base"); }
    public abstract void Bar();
}

class Derived : Base
{
    public override void Foo() { Console.WriteLine("Derived"); }
    public override void Bar() { Console.WriteLine("Must Implement!"); }
}
```
---

## Q52: What is lambda expressions in C#?
A lambda expression is an anonymous function that can be used to create delegates or expression tree types. Lambda expressions are a concise way to write inline functions, often used in LINQ queries, event handling, or for passing short bits of executable code. They use the `=>` syntax and can have parameters, a body expression, and/or code blocks.
```csharp
Func<int, int, int> add = (a, b) => a + b;
int sum = add(3, 4); // sum is 7

var evens = numbers.Where(n => n % 2 == 0);
```
---

## Q53: What is the difference between Equality Operator (==) and Equals() Method in C#?
The `==` operator tests for value equality, but its behavior depends on how it is overloaded; for reference types, it compares references unless overridden (e.g., in string it checks value). The `Equals()` method is virtual and can be overridden to test for value equality. It allows for type-specific equality checks, while `==` may not always provide the intended semantics if not properly overloaded.
```csharp
string a = "test";
string b = "test";
bool r1 = (a == b);        // true, since string overrides ==
bool r2 = a.Equals(b);     // true

object o1 = new object();
object o2 = new object();
bool r3 = (o1 == o2);      // false, compares reference
bool r4 = o1.Equals(o2);   // false, default reference comparison
```
---

## Q54: What is the use of Null Coalescing Operator (??) in C#?
The null coalescing operator `??` provides a compact way to assign a default value if a nullable type or reference type is null. If the left-hand operand is not null, it returns that value; otherwise, it returns the right-hand operand. It simplifies null-checking code and reduces verbosity.
```csharp
string name = null;
string displayName = name ?? "Unknown"; // displayName = "Unknown"
```
---

## Q55: What is Virtual Method in C#?
A virtual method is a method declared in a base class using the `virtual` keyword. It provides an implementation that can be overridden by any derived class using the `override` keyword. This allows for dynamic polymorphism, enabling derived classes to modify or extend the base class behavior.
```csharp
public class Base
{
    public virtual void Show() { Console.WriteLine("Base"); }
}
public class Derived : Base
{
    public override void Show() { Console.WriteLine("Derived"); }
}
```
---

# Senior

## Q56: What is difference between late binding and early binding in C#?
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

## Q57: What is the difference between Func<string, string> and delegate?
`Func<string, string>` is a built-in generic delegate representing a function taking a string parameter and returning a string. `delegate` is a keyword for defining custom delegate types, which can represent methods with specific signatures. `Func<>` provides concise syntax for common function signatures, while `delegate` is used for more specialized scenarios.
```csharp
Func<string, string> func = s => s.ToUpper();

delegate string MyDelegate(string input);
MyDelegate del = s => s.ToUpper();
```
---

## Q58: Is operator overloading supported in C#?
Yes, operator overloading is supported in C# for user-defined types. It allows you to define or modify the behavior of built-in operators (like +, -, ==, etc.) for custom types by declaring static methods with the `operator` keyword. Not all operators can be overloaded (e.g., `&&`, `||` require `&`, `|` overloading); overuse can affect code readability.
```csharp
public class Complex
{
    public int Real, Imaginary;
    public static Complex operator +(Complex a, Complex b)
        => new Complex { Real = a.Real + b.Real, Imaginary = a.Imaginary + b.Imaginary };
}
```
---

## Q59: Can Multiple Inheritance implemented in C#?
C# does not support multiple inheritance of classes (a class cannot inherit from more than one base class). However, C# allows multiple interface inheritance, where a class can implement any number of interfaces. This provides similar flexibility without ambiguity of member conflicts found in multiple class inheritance.
```csharp
public interface IA { void A(); }
public interface IB { void B(); }

public class MyClass : IA, IB
{
    public void A() {}
    public void B() {}
}
```
---

## Q60: What interface should your data structure implement to make the Where method work?
To make the `Where` method (from LINQ) work, your data structure should implement the `IEnumerable<T>` interface. LINQ operators such as `Where` are extension methods for `IEnumerable<T>`, enabling query capabilities on any collection or custom data structure that supports it.
```csharp
public class MyCollection<T> : IEnumerable<T>
{
    // Implement GetEnumerator()
    public IEnumerator<T> GetEnumerator() { /*...*/ }
    IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();
}
```
---

## Q61: What is a static constructor?

A static constructor in C# is used to initialize static members of a class or to perform actions that need to be executed only once for the entire class, regardless of how many instances are created. It is called automatically by the .NET runtime before any static members are accessed or any instance is created, and it cannot be called directly. A static constructor does not take any parameters and cannot have an access modifier—it's always private by default. It's commonly used to assign default values for static fields or perform logging, configuration, or resource initialization for static data. Since it runs only once during the lifetime of the application domain, it ensures the static data is properly initialized before use.

**Key points:**
- No parameters, no access modifier.
- Called once, automatically by the runtime.
- Used for initializing static members or performing class-level actions.

```csharp
class Example
{
    public static int StaticValue;

    static Example() // static constructor
    {
        StaticValue = 42; // Initialize static member
        Console.WriteLine("Static constructor called");
    }
}
```
---

## Q62: What is the use of conditional preprocessor directive in C#?

Conditional preprocessor directives in C# allow the compiler to compile or skip some code portions based on specific conditions. They're mainly used to include code only for certain build configurations, like DEBUG or RELEASE. The most common directives are `#if`, `#else`, `#elif`, `#endif`, and `#define`. This allows developers to control debugging, logging, platform-specific code, and experimental features without changing other code manually. Preprocessor directives only affect compilation and are removed from the final binary, making them powerful for cross-platform code, different feature sets, or additional debug information.

```csharp
#define DEBUG 
using System;

class Program
{
    static void Main()
    {
#if DEBUG
        Console.WriteLine("Debug mode is ON");
#else
        Console.WriteLine("Release mode");
#endif
    }
}
```
---

## Q63: Explain what is Ternary Search?

Ternary search is a searching algorithm used to find the maximum or minimum value of a unimodal function (a function that increases then decreases or vice versa) or to search in a sorted array, similar to binary search but dividing into three parts instead of two. It recursively splits the array or range into three equal parts and determines which segment the target lies in (for discrete search) or which segment has the extremum (for optimization). Ternary search has a time complexity of O(log₃N), which is slightly slower than binary search for general searching but useful in optimization problems, especially where the target is to find an optimal point rather than a specific value.

```csharp
// Ternary search for max in unimodal function
double TernarySearchMax(Func<double, double> f, double left, double right, double eps = 1e-6)
{
    while (right - left > eps)
    {
        double m1 = left + (right - left) / 3;
        double m2 = right - (right - left) / 3;
        if (f(m1) < f(m2))
            left = m1;
        else
            right = m2;
    }
    return (left + right) / 2;
}
```
---

## Q64: Explain how does Asynchronous tasks Async/Await work in .NET?

Async/await in .NET allows asynchronous programming by enabling methods to run operations without blocking the main thread. The `async` keyword marks a method as asynchronous, and `await` is used to pause the method's execution until the awaited task is complete. This makes it now possible to write easier-to-read, non-blocking code for I/O operations, network calls, etc. When an `await` is encountered, control returns to the caller while the awaited Task completes; once done, execution resumes after the await. Exceptions in async methods can be caught with try/catch. Async/await improves responsiveness in UI and scalability in web servers by not blocking threads.

```csharp
public async Task<string> GetDataAsync()
{
    HttpClient client = new HttpClient();
    string data = await client.GetStringAsync("http://example.com/api/values");
    return data;
}
```
---

## Q65: What happens when we Box or Unbox Nullable types?

When you box a nullable type (e.g., `int?`), if it contains a value, the contained value (e.g., int) is boxed, not the Nullable type itself. If the nullable has no value (`null`), a `null` reference is boxed. When unboxing, if the boxed value is `null`, unboxing to a Nullable type (`T?`) yields a Nullable instance with `HasValue=false`. Unboxing to a value type directly (`T`) will throw an `InvalidOperationException` if the boxed value was originally `null`.

```csharp
int? n = null;
object o = n; // o is null

int? n2 = 5;
object o2 = n2; // o2 is boxed int (5)

int? n3 = (int?)o2; // unbox, n3 == 5

int? n4 = (int?)o; // n4 == null

// int n5 = (int)o; // throws InvalidOperationException
```
---

## Q66: Can you explain the difference between Interface, abstract class, sealed class, static class and partial class in C#?

- **Interface:** Only declarations of methods, properties, etc., no implementation. Classes must implement all members.
- **Abstract class:** Can have both abstract members (no implementation) and implemented members. Cannot be directly instantiated, serves as a base class.
- **Sealed class:** Cannot be inherited. Used to prevent other classes from deriving from it.
- **Static class:** Cannot be instantiated, all members must be static. Used for utility methods and constants.
- **Partial class:** Definition can be split across multiple files for organizational purposes, compiled as one class.

```csharp
interface ITest { void DoWork(); } // Only signatures

abstract class AbstractBase { public abstract void DoWork(); }

sealed class FinalClass { }

static class UtilityClass { public static void Helper() { } }

partial class SplitClass { /* part 1 */ }
// In another file: partial class SplitClass { /* part 2 */ }
```
---

## Q67: How to solve Circular Reference?

Circular references happen when two or more objects reference each other, blocking garbage collection. This can lead to memory leaks. To solve circular references:
- Use weak references (WeakReference) for non-essential links.
- Break the circular references manually before disposal (set references to null).
- Design your classes to minimize or avoid mutual references.
- For serialization, use custom serialization strategies to prevent infinite loops.

```csharp
class A { public B RefB; }
class B { public A RefA; }

void BreakCircularRef(A a, B b)
{
    a.RefB = null;
    b.RefA = null;
}

// Or use WeakReference
class A2 { public WeakReference<B> RefB; }
```
---

## Q68: Test if a Number belongs to the Fibonacci Series

A number is in the Fibonacci series if and only if either `5*n*n + 4` or `5*n*n - 4` is a perfect square.

```csharp
bool IsFibonacci(int n)
{
    bool IsPerfectSquare(int x) => (int)Math.Sqrt(x) * (int)Math.Sqrt(x) == x;
    return IsPerfectSquare(5 * n * n + 4) || IsPerfectSquare(5 * n * n - 4);
}
```
---

## Q69: When to use ArrayList over array[] in C#?

Use `ArrayList` when you need a collection of objects whose size can change dynamically and when you are dealing with non-generic types or legacy code (pre-.NET 2.0). ArrayList provides dynamic resizing and convenience methods. However, it's not type-safe (stores objects), slower, and generally superseded by the generic `List<T>`. Use array[] when the size is fixed and for performance.

```csharp
ArrayList list = new ArrayList();
list.Add(1);
list.Add("hello"); // Accepts any type (not type-safe)

int[] arr = new int[10]; // static size, faster, type-safe
```
---

## Q70: IEnumerable vs List - What to Use? How do they work?

`IEnumerable<T>` is an interface for objects that can be enumerated (iterated over) one at a time. It enables deferred execution and is ideal for LINQ queries and read-only access. `List<T>` is a concrete class implementing ICollection<T>, IList<T>, and IEnumerable<T> with random access, dynamic resizing, and modification methods. Use IEnumerable for read-only or streaming data; use List when you need indexed access or to modify the collection.

```csharp
IEnumerable<int> numbers = Enumerable.Range(1, 10);

List<int> numList = new List<int>(numbers);
numList.Add(20);
int x = numList[2]; // List supports indexing
```
---

## Q71: When would you use delegates in C#?

Delegates are used in C# when you need to encapsulate a reference to a method with a specific signature, making it possible to treat methods as first-class objects. They are especially useful for designing extensible and flexible applications, where behavior needs to be passed as a parameter. Common use cases include event handling, callback methods, and implementing patterns like the observer or strategy pattern. Delegates enable decoupling between classes so that a method can be invoked without knowing the object or method's exact implementation. They are multicast, allowing multiple methods to be invoked in sequence. With the advent of anonymous methods and lambda expressions, using delegates has become more straightforward and expressive. Delegates play a crucial role in the event model of .NET (e.g., `EventHandler`). They are type-safe, ensuring that the signature matches at compile time. Delegates are also extensively leveraged in LINQ and asynchronous programming. Unlike interfaces, delegates can reference static and instance methods. They also work well for implementing generic reusable components that can interact through pre-defined behaviors.

```csharp
// Example: Passing a delegate as a callback
public delegate void Notify(string message);

public class Process
{
    public void Start(Notify notifyCallback)
    {
        notifyCallback("Processing started.");
    }
}

// Usage
Process process = new Process();
process.Start(msg => Console.WriteLine(msg));
```
---

## Q72: What are the different ways a method can be overloaded?

Method overloading in C# allows multiple methods with the same name but different parameter lists to coexist in the same class. There are several ways to overload a method:
1. Change the number of parameters (arity) in the method signature.
2. Change the type of parameters.
3. Change the order of parameters if they have different types.
4. Use different parameter modifiers (e.g., `ref`, `out`, `params`).
Return type alone cannot be used to overload a method; the compiler enforces overload resolution based solely on the parameter list. Overloading enhances code readability and maintainability by providing the same method name for similar operations that work on different types or parameter variations. It is commonly used in constructors and utility methods. Care should be taken to avoid confusion, especially when using optional parameters.

```csharp
public void Print(int number) { }
public void Print(string text) { }
public void Print(int number, string text) { }
public void Print(ref int number) { }
public void Print(params int[] numbers) { }
```
---

## Q73: What is the best practice to have best performance using Lazy objects?

The `Lazy<T>` type in C# enables deferred, thread-safe initialization of expensive objects. For the best performance, you should choose an appropriate thread-safety mode according to your application's needs. `LazyThreadSafetyMode.ExecutionAndPublication` (default) ensures thread safety, but if only a single thread accesses the lazy instance, `LazyThreadSafetyMode.None` is more efficient. Avoid unnecessary locking by choosing the least restrictive mode applicable. Initialize `Lazy<T>` with a value factory only if instantiation is expensive or resource-consuming. Avoid capturing large or unnecessary state in the factory delegate to prevent memory leaks. Also, ensure exceptions during initialization are handled appropriately, as they can be cached and thrown for subsequent accesses. Use `Lazy<T>` primarily for objects that are costly to create and not always needed, such as database connections or expensive computations. Consider memory usage, as `Lazy<T>` maintains state until garbage collected, even if accessed only once.

```csharp
// Example: Best practice with Lazy initialization
private static readonly Lazy<MyService> _service = 
    new Lazy<MyService>(() => new MyService(), LazyThreadSafetyMode.ExecutionAndPublication);

public MyService Service => _service.Value;
```
---

## Q74: What is scope of a Protected Internal member variable of a C# class?

A member marked as `protected internal` in C# is accessible from:
1. Any class in the same assembly (like `internal`).
2. Any derived class, even if it is in a different assembly (like `protected`).
This allows for a broader access than just `protected` or `internal` alone. The access is permitted if the accessing code is either in the same assembly or in a derived class, not necessarily both. `protected internal` is often used for base classes designed for inheritance and for use across a single assembly. However, it can make the access surface larger than generally desired, so it's best used carefully to avoid inadvertently exposing implementation details to unrelated code.

```csharp
public class BaseClass
{
    protected internal int data;
}

public class DerivedClass : BaseClass
{
    void Access()
    {
        data = 10; // Accessible here
    }
}
```
---

## Q75: What is Indexer in C#?

An indexer in C# allows an object to be indexed like an array, enabling access to internal data via an index. It is a special type of property defined with the `this` keyword and one or more parameters. Indexers make it possible to access class instances using array notation (`obj[index]`). This is useful for classes representing collections or containers, such as custom list or dictionary types. You can define multiple indexers with different parameter types or signatures (overloading). Indexers can have different accessibility for get and set accessors and support any valid data type for the index. They improve code readability and encapsulation, allowing controlled access to internal structures.

```csharp
public class SampleCollection<T>
{
    private T[] arr = new T[10];
    public T this[int i]
    {
        get { return arr[i]; }
        set { arr[i] = value; }
    }
}

// Usage
var collection = new SampleCollection<string>();
collection[0] = "Hello";
Console.WriteLine(collection[0]);
```
---

## Q76: Explain what is Short-Circuit Evaluation in C#?

Short-circuit evaluation in C# refers to the way logical operators `&&` (AND) and `||` (OR) evaluate expressions. With `&&`, if the left-hand operand is `false`, the right-hand side is not evaluated because the whole expression cannot be `true`. Similarly, with `||`, if the left-hand operand is `true`, the right-hand operand is skipped. This behavior improves efficiency and can prevent errors, such as null reference exceptions when accessing properties or methods on potentially null objects. It's commonly used in conditions to safely check for nulls before accessing members. Note that bitwise operations `&` and `|` do not short-circuit and always evaluate both sides.

```csharp
string s = null;
if (s != null && s.Length > 0)
{
    // Will not throw NullReferenceException because s.Length is not evaluated if s is null.
}
```
---

## Q77: Can you create a function in C# which can accept varying number of arguments?

Yes, C# supports parameter arrays using the `params` keyword, allowing a function to accept a variable number of arguments of a specified type. This is useful when the exact number of parameters is unknown, such as mathematical aggregation functions or logging methods. Only one `params` parameter is allowed, and it must be the last in the parameter list. The function can be called with zero, one, or many arguments, or even an explicit array. Overloading with and without `params` is allowed for maximum flexibility.

```csharp
public void PrintNumbers(params int[] numbers)
{
    foreach (int num in numbers)
        Console.WriteLine(num);
}

// Usage
PrintNumbers(1, 2, 3);
PrintNumbers(); // works
PrintNumbers(new int[] { 10, 20 });
```
---

## Q78: What is Marshalling and why do we need it?

Marshalling is the process of transforming data types when communicating across different programming environments, such as managed (.NET) and unmanaged (native) code. It's necessary because managed and unmanaged environments may represent data differently in memory. Marshalling ensures the correct exchange of data between managed code (e.g., C#) and unmanaged APIs (e.g., Win32 DLLs, COM components), handling datatype conversions, pointer mappings, and memory allocations automatically or via explicit attributes. Without marshalling, calling native code from managed applications or vice versa would result in data loss, corruption, or crashes. In C#, marshalling is frequently used with the `DllImport` attribute for P/Invoke.

```csharp
[DllImport("user32.dll", CharSet = CharSet.Unicode)]
public static extern int MessageBox(IntPtr hWnd, string text, string caption, uint type);
```
---

## Q79: What is the difference between is and as operators in C#?

The `is` operator checks if an object is compatible with a given type and returns a boolean. The `as` operator attempts to cast an object to a given type, returning `null` if the cast fails instead of throwing an exception. `is` is useful for type checking before casting, especially with pattern matching. `as` is used for safe reference or nullable type conversions without risking invalid cast exceptions. Note that `as` works only with reference types or nullable types, not value types.

```csharp
object obj = "Hello";
if (obj is string) { /* true */ }

string s = obj as string; // s != null
```
---

## Q80: What are pointer types in C#?

Pointer types in C# allow direct memory address manipulation, similar to C/C++. A pointer is a variable that holds the address of another variable. Using pointers requires `unsafe` context, and is generally used for interoperability, high-performance scenarios, or system programming. Pointer types are declared using the `*` symbol, e.g., `int* ptr;`. Pointers can be used to access and manipulate memory directly, which bypasses type safety and memory management provided by .NET, so their use is restricted to trusted code and often disabled by default. Pointer arithmetic, dereferencing, and array pointer manipulation are possible with pointers. They are not allowed on reference types, except for strings with special handling.

```csharp
unsafe
{
    int value = 10;
    int* p = &value;
    Console.WriteLine(*p); // prints 10
    *p = 20;
}
```
---

## Q81: What is the yield keyword used for in C#?

The yield keyword in C# is used within an iterator method to provide a value to the enumerator object one at a time. This allows you to define custom iteration behavior in a lazy way, generating elements of a collection on demand rather than creating and returning a complete collection at once. When the yield return statement is reached, the current location in the method is stored, and execution resumes from this point the next time the iterator is called. This is particularly useful when traversing large collections or generating sequences where you may not want or need all the results at once. Using yield can also improve performance and reduce memory usage, as no intermediate collections are created. It's commonly used in implementing enumerators for custom collections and writing generator functions. There is also yield break used to signal the end of iteration. Methods using yield must return IEnumerable, IEnumerable<T>, IEnumerator, or IEnumerator<T>. When using yield, you cannot have ref or out parameters in the method signature, and you cannot use yield inside anonymous methods or lambda expressions.

```csharp
public IEnumerable<int> GetEvenNumbers(int max)
{
    for (int i = 0; i <= max; i++)
    {
        if (i % 2 == 0)
            yield return i;
    }
}
```
---

## Q82: What's the difference between StackOverflowError and OutOfMemoryError?

Although the names are similar, StackOverflowError and OutOfMemoryError indicate different problems in C#. StackOverflowException occurs when the stack, a memory region used for function calls and local variables, exceeds its limit. This typically happens with uncontrolled or excessive recursion, causing each new function call to consume more stack space until it's exhausted. On the other hand, OutOfMemoryException is thrown when the managed heap, used for dynamic memory allocation (objects, arrays, etc.), cannot fulfill a memory request usually due to fragmentation, memory leaks, or genuinely running out of physical RAM. StackOverflowException cannot be caught reliably, and the process usually terminates. OutOfMemoryException can be caught, though it's often hard to recover safely after it occurs. Preventing StackOverflow requires careful recursion, and avoiding OutOfMemory requires managing allocations and ensuring objects are disposed. Both are critical runtime errors but in different memory regions: StackOverflow relates to call stack capacity, and OutOfMemory to the heap.

```csharp
// StackOverflow example
void Recursive() { Recursive(); } // Calling this method will cause StackOverflowException

// OutOfMemory example
List<byte[]> list = new List<byte[]>();
while (true) { list.Add(new byte[1024 * 1024]); } // Eventually causes OutOfMemoryException
```
---

## Q83: Why to use lock statement in C#?

The lock statement in C# is used to ensure that a critical section of code is executed by only one thread at a time, providing thread safety. Without locks, if multiple threads access shared resources simultaneously, it can lead to race conditions, data corruption, or unpredictable results. Locks act by acquiring a mutual-exclusion lock for an object, preventing other threads from entering the block of code until the lock is released. This is widely used in multithreaded applications when updating shared data, e.g., collections, counters, or writing files. It's important to avoid locking on public objects or string literals, use private objects for locks, and keep the lock duration short to reduce contention and avoid deadlocks. Overusing locks can affect performance due to increased blocking, so use lock only when necessary. The lock is syntactic sugar for Monitor.Enter/Exit, handling exceptions and unlocking reliably.

```csharp
private object _lockObj = new object();
private int _counter;

public void ThreadSafeIncrement()
{
    lock(_lockObj)
    {
        _counter++;
    }
}
```
---

## Q84: Explain the difference between Select and Where.

Select and Where are both LINQ extension methods but serve distinct purposes. Where is used to filter elements from a collection based on a predicate (condition), returning only items that satisfy this condition. Select is for projecting each element of a collection into a new form, transforming data but keeping collection size the same. Where preserves the original elements, Select can change the type or structure. For example, Where could extract even numbers, while Select could square each number or convert objects to DTOs. Multiple Select and Where calls can be combined to filter and transform data in a flexible way. It's important to note that both methods use deferred execution: no iteration happens until results are enumerated.

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
var evens = numbers.Where(n => n % 2 == 0);           // Filters: 2, 4
var squares = numbers.Select(n => n * n);             // Projects: 1, 4, 9, 16, 25
```
---

## Q85: What is the difference between dispose and finalize methods in C#?

Dispose and Finalize are both mechanisms for resource cleanup, but they serve different purposes and are used differently. Dispose is a public method of the IDisposable interface and is called explicitly by code to free unmanaged resources (like file handles, database connections) when they're no longer needed. Finalize is implemented using a destructor (~ClassName()), automatically called by the garbage collector before the object is reclaimed, but with no guaranteed timing. Dispose provides deterministic cleanup, allowing immediate resource release, while Finalize provides a safety net in case Dispose wasn't called. You should implement Dispose when your class manages unmanaged resources, and call Dispose manually or via a using statement. Implement Finalize only when absolutely necessary, as it introduces overhead, and always suppress finalization (GC.SuppressFinalize) after Dispose has been called to avoid double-freeing resources. Most resource types should avoid reliance on finalization, preferring Dispose.

```csharp
public class MyResource : IDisposable
{
    public void Dispose()
    {
        // Cleanup resources
        GC.SuppressFinalize(this);
    }

    ~MyResource()
    {
        // Finalizer logic (if needed)
    }
}
```
---

## Q86: What is the Constructor Chaining in C#?

Constructor chaining refers to the process where one constructor calls another constructor in the same class or a base class to reuse initialization logic, reducing code duplication and improving maintainability. In a class, you use the this keyword to chain to another constructor in the same class, or the base keyword to call a constructor from a parent class. This is useful when you have multiple constructors with different parameters but shared logic, so the common setup is centralized in one constructor. C# enforces that constructor initializer (this or base) must be the first statement. Chaining enhances code clarity and makes maintaining initialization logic easier, especially with classes with several ways to instantiate. It’s common in both inheritance and overloaded constructors.

```csharp
public class Person
{
    public string Name;
    public int Age;

    public Person() : this("Unknown", 0) { }
    public Person(string name) : this(name, 0) { }
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
```
---

## Q87: What is the difference between System.ApplicationException class and System.SystemException class?

System.ApplicationException and System.SystemException are both derived from the Exception base class but are intended for different purposes. System.SystemException is the base for all exceptions thrown by the .NET runtime, such as NullReferenceException, IndexOutOfRangeException, etc. It's used to distinguish exceptions that originate from system-level errors and underlying runtime issues. System.ApplicationException, on the other hand, is intended to be the base class for custom exceptions defined by user applications. Microsoft now discourages using ApplicationException directly; instead, it's best practice to derive custom exceptions directly from Exception. SystemException and its descendants represent critical runtime failures, while ApplicationException was for application-level exceptions but is rarely used in practice. Handling should be more specific, not catching SystemException broadly.

```csharp
// Custom application exception (modern approach)
public class MyCustomException : Exception
{
    public MyCustomException(string message) : base(message) { }
}
```
---

# Expert

## Q88: Why doesn't C# allow static methods to implement an interface?

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

## Q89: Could you explain the difference between destructor, dispose and finalize method?

A destructor in C# (`~ClassName()`) is a special syntax for a finalizer method, called by the garbage collector before the object is destroyed. Dispose is a method of the IDisposable interface, meant to be called manually to perform deterministic cleanup of unmanaged resources. Finalize is the underlying mechanism that the destructor syntax compiles to; it's automatically called by the CLR but only for non-deterministic cleanup. Use Dispose for immediate, predictable cleanup, such as closing files or releasing database connections. Use a finalizer only as a last-resort safety net if Dispose isn’t called, but doing so is discouraged due to performance costs and unpredictability. If both are present, Dispose should suppress finalization using `GC.SuppressFinalize`. Unlike destructors/finalizers, Dispose is explicitly called (via using or manually), and never called by the garbage collector. Well-designed classes should implement IDisposable and avoid finalizers unless necessary.

```csharp
public class Example : IDisposable
{
    ~Example()
    {
        // Destructor / Finalizer logic
    }
    public void Dispose()
    {
        // Deterministic cleanup
        GC.SuppressFinalize(this);
    }
}
```
---

## Q90: Explain the difference between IQueryable, ICollection, IList & IDictionary interfaces?

IQueryable allows querying data sources using LINQ at a higher level, supporting query translation for remote data sources (like databases) and deferred execution. ICollection represents a generic collection of objects, providing methods for counting, adding, removing, and checking for existence, and is the base for many collection types. IList extends ICollection, adding access by index and the ability to insert or remove elements at specific positions—it's used for collections where ordering and random access matters. IDictionary represents a collection of key-value pairs, supporting fast lookups and access by key rather than index. Typically, use ICollection for generic collections, IList for list-like collections with order/indexes, and IDictionary when you need lookups by key. IQueryable is mostly for remote or queryable sources, supporting LINQ expression trees that may be executed outside the .NET process (e.g., SQL databases).

```csharp
IList<int> list = new List<int> {1, 2, 3};
IDictionary<string, int> dict = new Dictionary<string, int>();
ICollection<int> collection = list;
IQueryable<int> query = list.AsQueryable();
```
---

## Q91: Can you add extension methods to an existing static class?

No, you cannot add extension methods directly to an existing static class itself in C#. Extension methods are special static methods for extending instances of types (usually non-static). They must reside in a static, non-nested class and have the first parameter marked with `this`, referring to the type they extend. Since static classes cannot be instantiated and have only static members, extension methods cannot be invoked on them—they require an instance to extend. Extension methods only augment instance methods; they can't be static methods of other static classes. However, extension methods can be declared for static members (types), but the syntax to call them isn't supported. Therefore, static classes can't be practically extended with extension methods.

```csharp
public static class StringExtensions
{
    public static bool IsNumeric(this string value)
    {
        return int.TryParse(value, out _);
    }
}

// Usage:
bool result = "123".IsNumeric();
```
---

## Q92: What is the difference between Lambdas and Delegates?

Delegates are types that reference methods with specific signatures, enabling methods to be assigned to variables and passed as arguments, thus supporting callback and event models. Lambdas are concise syntaxes for creating anonymous functions, often used to instantiate delegates inline. Delegates can reference methods declared elsewhere (named methods), while lambdas typically express behavior in place, improving code readability and reducing boilerplate. Lambdas may capture variables from their enclosing scope (closures). Both support type inference and are fully interoperable. Lambdas are primarily a syntax improvement that generate delegate instances behind the scenes. Delegates as types are broader concepts; lambdas make applying them more powerful and convenient.

```csharp
delegate int Operation(int x, int y);

Operation addDel = (x, y) => x + y;        // Lambda assigned to delegate
int result = addDel(3, 4);                 // result = 7
```
---

## Q93: What is a preprocessor directives in C#?

Preprocessor directives in C# are special instructions for the compiler, indicated with a `#` at the start of a line, such as `#define`, `#if`, `#else`, `#elif`, `#endif`, `#region`, `#endregion`, `#warning`, and `#error`. They are processed before compilation and can be used to conditionally compile code, include or exclude code segments, organize code, or issue warnings and errors at compile time. Although not as powerful as in C or C++, C# preprocessor directives are commonly used for compiling code based on build configuration (e.g., DEBUG/RELEASE) or platform. They do not affect runtime behavior, only what is compiled into the application, and are especially useful for debugging or platform-specific optimizations.

```csharp
#define DEBUG
#if DEBUG
    Console.WriteLine("Debug mode");
#else
    Console.WriteLine("Release mode");
#endif
```
---

## Q94: In C#, when should we use abstract classes instead of interfaces with extension methods?

Use abstract classes when you want to provide a base level of implementation, enforce inheritance, include shared state (fields), or protect implementation details. Abstract classes can define non-abstract (fully implemented) members, constructors, fields, and properties, supporting “IS-A” relationships and code reuse through inheritance. Interfaces with extension methods only allow you to define contracts (no shared state), and extension methods can’t access private members or override actual implementations; they act as syntactic sugar for utility methods. Abstract classes are preferable when future expansion, base logic sharing, versioning, or default implementation with possible overrides is necessary. Interfaces (with or without extension methods) are ideal for polymorphic contracts, multiple inheritance, and maximum flexibility.

```csharp
abstract class Animal
{
    public abstract void Speak();
    public void Eat() { /* Shared logic */ }
}

interface IWorker
{
    void Work();
}
static class WorkerExtensions
{
    public static void Rest(this IWorker w) { /* ... */ }
}
```
---

## Q95: What is the method MemberwiseClone() doing?

MemberwiseClone() is a protected method of the System.Object class that creates a shallow copy of the current object. It copies the non-static fields of the current object to a new object of the same type; for value types, fields are copied by value, and for reference types, the references are copied but not the objects themselves. This means the original and cloned objects share references to the same nested objects. It's commonly used for cloning where deep copying (recursively cloning all nested reference types) is not required. Since it's protected, you typically call it from within a class to implement ICloneable or a custom Clone() method. For deep cloning, you must implement additional logic to recursively clone referenced objects.

```csharp
public class Person
{
    public string Name;
    public Person Clone()
    {
        return (Person)this.MemberwiseClone();
    }
}
```
---

## Q96: Implement the Where method in C#. Explain.

The Where method is a LINQ extension method that filters elements of a sequence based on a predicate. In its basic form, Where iterates over an IEnumerable<T> and yields only those elements that satisfy the given condition. It uses deferred execution, meaning elements are not filtered until the result is enumerated. This design keeps memory and processing efficient.

```csharp
public static IEnumerable<T> Where<T>(this IEnumerable<T> source, Func<T, bool> predicate)
{
    foreach (var item in source)
    {
        if (predicate(item))
            yield return item;
    }
}
```
---

## Q97: Explain when to use Finalize vs Dispose?

Use Dispose when you want deterministic cleanup of resources, especially unmanaged resources (e.g., file handles, database connections), by explicitly calling or via a using statement. Dispose is defined by the IDisposable interface and should be called to release resources as soon as they are no longer needed. Finalize, implemented with a destructor (~ClassName()), is intended to clean up resources if Dispose was not called, but the timing is unpredictable—it runs when the garbage collector decides to reclaim the object. Always prefer Dispose for timely cleanup and only use Finalize as a backup, implementing it if your class directly manages unmanaged resources or must guard against finalization by derived classes. If both are used, Dispose should call GC.SuppressFinalize to prevent double cleanup.

```csharp
public class ResourceHolder : IDisposable
{
    ~ResourceHolder() { /* Finalizer logic (rarely needed) */ }
    public void Dispose()
    {
        // Resource cleanup
        GC.SuppressFinalize(this);
    }
}
```
---

## Q98: What is the volatile keyword used for?

The volatile keyword in C# is used to indicate that a field may be modified by multiple threads, and prevents compiler, CLR, and processor optimizations that assume access by a single thread. Declaring a field as volatile ensures that reads and writes to that field are always done directly from memory, providing the most recent value. It is generally used with flags and simple types to synchronize access in multithreaded scenarios without explicit locks. Volatile is not sufficient for complex thread synchronization, but helps with simple state variables shared between threads. It cannot be applied to every field type (e.g., not for arrays or double-locking patterns). Its main benefit is predictable cross-thread visibility of variable state.

```csharp
private volatile bool _doWork = true;

public void StopWork()
{
    _doWork = false;
}
```
---

## Q99: What are Circular References in C#?

Circular references occur when two or more objects reference each other, forming a loop in the reference graph. For example, Object A references Object B, and Object B references Object A. In garbage-collected environments like C#, the garbage collector can handle most circular references if there are no external references; the entire cycle is eligible for collection. However, circular references can cause problems when unmanaged resources or event handlers are involved, preventing object destruction and resulting in memory leaks. Special care is needed to break such cycles manually or use weak references where appropriate. In serialization and data graphs, circular references lead to stack overflows or serialization errors—frameworks may throw exceptions or require special handling.

```csharp
class Node
{
    public Node Next;
    public Node Previous;
}
```
---

## Q100: Could you explain the difference between Func vs. Action vs. Predicate?

Func, Action, and Predicate are delegates in C# used for encapsulating methods with specific signatures. **Func** represents a method that returns a value and can have 0 or more input parameters. The last parameter is always the return type; for example, `Func<int, int, int>` takes two integers and returns an integer. **Action** represents a method that does not return a value (void) and can have 0 or more input parameters; for instance, `Action<string>` takes a string parameter and returns void. **Predicate** is a specialized delegate representing methods that return a boolean and take exactly one parameter; it’s used commonly for searching or filtering collections.

The main advantage of using these delegates is to increase code flexibility and allow methods to be passed as arguments for higher-order functions. Func is ideal for mapping and transforming data, Action for actions like logging or updating, and Predicate for criteria checks. They are heavily used in LINQ methods.

```csharp
// Func example
Func<int, int, int> add = (x, y) => x + y;
int sum = add(2, 3); // sum = 5

// Action example
Action<string> greet = name => Console.WriteLine($"Hello, {name}!");
greet("Alice");

// Predicate example
Predicate<int> isEven = x => x % 2 == 0;
bool result = isEven(4); // true
```
---

## Q101: You have defined a destructor in a class that you have developed by using the C#, but the destructor never executed. Why?

In C#, a destructor (finalizer) is not called immediately when an object goes out of scope or is no longer used. Instead, it is executed by the garbage collector (GC) at an indeterminate time, if at all, before the application exits. If the GC does not finalize an object (e.g., if the application closes before the GC runs or the object survives for the lifetime of the process), the destructor may never be called.

Other reasons a destructor might not execute include: the program ends before the GC runs a collection on the object; the object is still referenced; or the application is terminated abruptly (e.g., Environment.FailFast or process kill). Deterministic cleanup should use IDisposable and Dispose method rather than relying on destructors, which are non-deterministic.

```csharp
class MyClass
{
    ~MyClass()
    {
        Console.WriteLine("Destructor called");
    }
}

// May never see "Destructor called" if the GC doesn't collect the object before program ends
```
---

## Q102: List some different ways for equality check in .NET

Equality checking in .NET can be performed using several approaches based on reference or value semantics:

1. **Equality Operator (`==`)** – Checks for value equality for value types, often reference equality for reference types unless overloaded.
2. **Object.Equals()** – Can be overridden for custom equality logic; used for both value and reference types.
3. **ReferenceEquals()** – Checks if two references point to the same object in memory.
4. **IEquatable<T>.Equals()** – Interface for custom equality logic, often recommended for collections and generics.
5. **SequenceEqual()** (LINQ) – Compares sequences (collections, arrays) for elementwise equality.
6. **EqualityComparer<T>.Default.Equals()** – Standard way for comparing elements, especially in collections or generics.
7. **CompareTo()** – Used for ordering but can indicate equality.

Each method is suitable for specific scenarios: primitive types, custom objects, or collections.

```csharp
int a = 5, b = 5;
bool valueEquality = (a == b);

object obj1 = new object(), obj2 = obj1;
bool referenceCheck = Object.ReferenceEquals(obj1, obj2);

string s1 = "test", s2 = "test";
bool equalsCheck = s1.Equals(s2); // True for string content

List<int> l1 = new List<int> { 1, 2 }, l2 = new List<int> { 1, 2 };
bool listEquals = l1.SequenceEqual(l2); // True
```
---

## Q103: What is Multicast Delegate in C#?

A multicast delegate is a delegate that holds references to, and can invoke, multiple methods. This is possible because delegates in C# are multicast by default (as long as the return type is void). When invoked, a multicast delegate calls its associated methods in the order they were added. Only the result of the last method is returned (for non-void delegates), but all methods' side effects occur.

Multicast delegates are useful for event handling, where multiple subscribers need to be notified of an event. Methods can be added or removed from the invocation list using `+=` and `-=`. If an exception occurs in one of the methods, the subsequent ones are not called unless handled.

```csharp
public delegate void Notify();

void First() { Console.WriteLine("First"); }
void Second() { Console.WriteLine("Second"); }

Notify notify = First;
notify += Second;
notify(); // Output: First \n Second
```
---

## Q104: What is the use of static constructors?

Static constructors in C# are used to initialize static members of a class or to perform actions that need to be performed only once. They run automatically before any static member is accessed, or the first instance is created, ensuring global initialization logic is executed only once. A static constructor cannot have access modifiers or parameters and can't be called explicitly.

They are ideal for initializing static fields, configuring logging, or loading configuration data needed for the type. The runtime ensures thread safety, so the static constructor is executed at most one time per application domain, before any static access occurs.

```csharp
class MyClass
{
    public static int Value;

    static MyClass()
    {
        Value = 42; // Static initialization
        Console.WriteLine("Static constructor called");
    }
}

// MyClass.Value; // Triggers static constructor
```
---

## Q105: What is jagged array in C# and when to prefer jagged arrays over multi-dimensional arrays?

A jagged array in C# is an array of arrays, meaning each "row" can be a different size and hold different arrays as elements. Unlike multi-dimensional arrays (rectangular arrays), which have fixed row and column sizes, jagged arrays give you flexibility in defining different lengths for each array's elements. You declare them using two sets of square brackets (e.g., `int[][]`).

Jagged arrays should be preferred when you need to store data where rows can have different numbers of elements, such as storing variable-length records or a triangle matrix. They're also more memory efficient in sparse data scenarios, as you only allocate the necessary elements.

```csharp
int[][] jagged = new int[3][];
jagged[0] = new int[2] { 1, 2 };
jagged[1] = new int[3] { 3, 4, 5 };
jagged[2] = new int[1] { 6 };

// Access: jagged[1][2] -> 5
```
---

## Q106: What are the differences between IEnumerable and IQueryable?

`IEnumerable` and `IQueryable` are interfaces for querying data, but they serve different purposes:

- `IEnumerable` is used for in-memory collections, enabling simple iteration over a collection (like a list or array). Operations on `IEnumerable` are applied once the data is already loaded into memory, and queries are executed as soon as the iteration begins.
- `IQueryable` is used for querying data sources that support query translation, like databases (LINQ-to-SQL, Entity Framework). It allows building and composing expression trees, which can be translated into SQL or other queries and executed on the server. This enables deferred execution and potentially more efficient queries, as only the filtered data is retrieved.

Use `IEnumerable` for in-memory processing and when the data is already available, whereas use `IQueryable` for performing database or remote queries where composition and efficiency are important.

```csharp
IEnumerable<int> numbers = new List<int> { 1, 2, 3 };
IQueryable<int> queryableNumbers = numbers.AsQueryable();

// IEnumerable iteration
foreach (var n in numbers) { /* ... */ }

// IQueryable supports remote query translation
var filtered = queryableNumbers.Where(x => x > 1);
```
---

## Q107: What are the benefits of a Deferred Execution in LINQ?

Deferred Execution in LINQ means that queries are not executed at the time of their declaration but are executed when the data is actually accessed (e.g., during enumeration). This provides several benefits:

1. **Performance:** Data is fetched and processed only when needed, saving memory and processing time if the results are never accessed.
2. **Composability:** Queries can be built in multiple steps, and the final query is executed only once, often as a single optimized operation.
3. **Resource Optimization:** Especially for databases, only the requested data is returned, reducing network and memory usage.
4. **Latest Data:** Deferred execution ensures that the most up-to-date data is retrieved at the point of enumeration.
5. **Efficiency in Chaining:** Multiple LINQ operations can be chained together without creating intermediate collections.

However, be cautious with side effects and external data sources, as the data may change between query definition and execution.

```csharp
IEnumerable<int> numbers = new List<int> { 1, 2, 3 };
var query = numbers.Where(x => x > 1); // Not executed yet

// Now, execution happens
foreach(var n in query)
{
    Console.WriteLine(n);
}
```
---

## Q108: Why Abstract class can not be sealed or static?

An abstract class in C# is intended to be a base class that cannot be instantiated directly and is designed to provide incomplete implementation for its derived types. A sealed class, on the other hand, is one that cannot be inherited; once marked sealed, no class can derive from it.

If an abstract class were allowed to be sealed, it would be impossible to both prevent instantiation and also prevent inheritance, which defeats the abstract class purpose. Similarly, an abstract class cannot be static because static classes cannot be instantiated or inherited, and all their members must be static, which is contrary to abstract members requiring overrides in derived types.

Thus, C# does not allow combining abstract with sealed or static since their design purposes are mutually exclusive.

```csharp
// Invalid in C#:
abstract sealed class Example {} // Error
abstract static class Example2 {} // Error
```
---

## Q109: Explain what is Weak Reference in C#?

A Weak Reference in C# is a reference type that allows the garbage collector (GC) to collect the referenced object while still allowing the application to access the object if it's still alive. Unlike a strong reference, holding a weak reference to an object does not prevent it from being garbage collected.

Weak references are especially useful in caching scenarios, where you want to keep objects alive if memory permits but allow the GC to reclaim them if memory usage becomes high. They help avoid memory leaks in long-lived applications where objects might otherwise remain referenced indefinitely.

You use the `WeakReference` class to create a weak reference. You need to check if the object is still alive before accessing it, as it may have been collected by the GC.

```csharp
MyObject obj = new MyObject();
WeakReference weakRef = new WeakReference(obj);
obj = null; // Now only a weak reference exists

if (weakRef.IsAlive)
{
    MyObject cachedObj = (MyObject)weakRef.Target;
    // Use cachedObj
}
```
---

## Q110: What's the difference between the System.Array.CopyTo() and System.Array.Clone()?

Both `System.Array.CopyTo()` and `System.Array.Clone()` are used to duplicate array data, but they operate differently:

- **CopyTo()** copies all elements from the source array to an existing target array, starting at a specified index. The target array must be at least large enough to hold the copied elements. It's a shallow copy: the elements themselves are not cloned, just copied by reference (for reference types).
- **Clone()** creates a new array instance of the same length and element type, copies all elements into it, and returns the new array as an object. It also creates a shallow copy, meaning the elements themselves are not duplicated for reference types—only the references are copied.

Use `Clone()` when you want a new independent array with the same contents, and `CopyTo()` when you want to copy elements into an existing array.

```csharp
int[] arr = { 1, 2, 3 };
int[] arr2 = new int[3];
arr.CopyTo(arr2, 0); // arr2: [1, 2, 3]

int[] arr3 = (int[])arr.Clone(); // arr3: [1, 2, 3]
```
---

## Q111: What is deep or shallow copy concept in C#?

A shallow copy copies the immediate fields of an object, but does not recursively copy objects referenced by those fields—it simply copies the reference, so both objects point to the same nested objects. A deep copy creates a new object and copies all objects referenced by the fields recursively, so nested objects are duplicated, and changes to one do not affect the other. In C#, Object.MemberwiseClone() provides a shallow copy. Deep copies often require custom code or serialization when objects contain references to other mutable objects.

```csharp
class Person { public string Name; }
Person a = new Person { Name = "Alice" };
Person b = (Person)a.MemberwiseClone(); // Shallow: b.Name refers same string
// For deep copy, you must create new Person and assign a copy of Name
```
---
