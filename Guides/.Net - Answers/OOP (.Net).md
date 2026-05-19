# Entry

## Q1: What is Inheritance?
Inheritance is a core OOP concept where a class (called a derived or child class) acquires the properties and behaviors (fields and methods) of another class (called a base or parent class). It enables code reusability and hierarchical classification. In C#, inheritance is implemented using the : symbol after the derived class name. The child class inherits accessible members (protected and public, not private) of the base class and can also add its own members or override base class members to provide specific functionality. Inheritance supports the "is-a" relationship, making it easier to create logical class hierarchies and foster maintainability.

```csharp
class Animal
{
    public void Eat() 
    {
        Console.WriteLine("Animal eats");
    }
}

class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Dog barks");
    }
}
```
---

## Q2: What is Object-Oriented Programming (OOP)?
Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects", which combine data (fields/properties) and behaviors (methods/functions) into a single unit. OOP promotes principles such as encapsulation, inheritance, polymorphism, and abstraction that help organize code into reusable, modular, and maintainable structures. Each object represents an instance of a class and interacts with other objects. This approach makes it easier to manage large codebases, supports code reuse, and aligns better with real-world concepts by modeling entities as objects.

```csharp
class Car
{
    public string Model { get; set; }
    public void Drive()
    {
        Console.WriteLine("Car is driving");
    }
}
Car myCar = new Car();
myCar.Drive();
```
---

# Junior

## Q3: What is the difference between a class and a structure?
A class is a reference type, while a structure (struct) is a value type in C#. Classes are allocated on the heap and support features like inheritance, polymorphism, and can have destructors. Classes can have null values since they are references. Structs are stored on the stack, cannot inherit from another struct or class (other than from System.ValueType), and cannot have a parameterless constructor or destructor. Structs are generally used for small, lightweight objects, while classes are suitable for complex entities requiring inheritance or reference semantics.

```csharp
class Person
{
    public string Name;
}

struct Point
{
    public int X, Y;
}
```
---

## Q4: Why is the virtual keyword used in code?
The virtual keyword is used to mark a method, property, or indexer in a base class as overridable in a derived class. It allows derived classes to provide a specific implementation of the method, property, or indexer using the override keyword. Without virtual, base class members cannot be overridden. This enables polymorphic behavior, where a base reference can call overridden methods in derived types, making systems more flexible and extensible.

```csharp
class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Animal speaks");
    }
}
class Cat : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Cat meows");
    }
}
```
---

## Q5: Can you inherit private members of a class?
Private members of a class are not inherited directly. They exist in the derived object, but are inaccessible from derived classes. Only public and protected members can be accessed or overridden by derived classes. Private fields and methods are encapsulated within the class they are defined in, ensuring proper data hiding. However, the derived class can access protected members and all accessible public members.

```csharp
class Base
{
    private int secret = 42;   // Not accessible in child
    protected int answer = 10; // Accessible in child
}
class Derived : Base
{
    void Display()
    {
        // Cannot access 'secret' here!
        Console.WriteLine(answer); // Can access 'answer'
    }
}
```
---

## Q6: Explain the concept of Constructor
A constructor is a special method in a class or struct that initializes a new object of that type. It has the same name as the class, does not have a return type (not even void), and is invoked automatically when an instance is created. Constructors can be parameterless (default) or take parameters to initialize fields. Constructors can also be overloaded to provide multiple ways of instantiating objects. Inheritance allows derived classes to call base class constructors with the base keyword.

```csharp
class Car
{
    public string Model;
    public Car(string model)
    {
        Model = model;
    }
}
Car myCar = new Car("Toyota");
```
---

## Q7: What is the difference between procedural and object-oriented programming?
Procedural programming organizes code as a sequence of instructions and typically uses functions and procedures to perform operations on data. Data and behavior are separate. In contrast, object-oriented programming (OOP) encapsulates data and behavior in objects, allowing for reusable and modular design. OOP supports abstraction, encapsulation, inheritance, and polymorphism. Procedural code tends to be less reusable and harder to maintain as complexity grows.

```csharp
// Procedural style
int Add(int a, int b) => a + b;

// OOP style
class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }
}
```
---

## Q8: What is Encapsulation?
Encapsulation is the OOP concept of bundling data (fields) and methods (functions) that operate on the data into a single unit (class) and restricting direct access to some of the object's components. This is typically done using access modifiers (private, public, protected). Encapsulation hides the internal state of the object from the outside, exposing only necessary parts through well-defined interfaces (methods or properties), thus improving security and integrity.

```csharp
class Account
{
    private decimal balance;
    public void Deposit(decimal amount)
    {
        if (amount > 0)
            balance += amount;
    }
    public decimal GetBalance() => balance;
}
```
---

## Q9: What is Polymorphism?
Polymorphism means "many forms" and refers to the ability in OOP to access objects of different types through a common interface or base class. In C#, it is achieved via method overriding and interfaces, enabling the same method call to behave differently depending on the runtime type of the object. This enhances code flexibility and extensibility by allowing behavior to be selected at runtime.

```csharp
class Shape
{
    public virtual void Draw()
    {
        Console.WriteLine("Drawing shape");
    }
}
class Circle : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing circle");
    }
}
Shape s = new Circle();
s.Draw(); // Output: "Drawing circle"
```
---

## Q10: What is an object?
An object is an instance of a class. It represents a specific implementation of the class template, containing both data (in fields/properties) and behaviors (methods). Objects are created in memory using the new keyword in C#. Each object can have different values for its data members, and can call its methods to perform actions. Objects enable encapsulation of state and behavior, and multiple objects of the same class can coexist with their unique states.

```csharp
class Student
{
    public string Name;
}
Student alice = new Student();
alice.Name = "Alice";
```
---

## Q11: What is a class?
A class is a blueprint or template that defines the shape and behavior of objects. It specifies what data (fields, properties) and operations (methods) the objects created from it will have. A class itself does not occupy memory until an object is created from it. Classes support inheritance, encapsulation, abstraction, and polymorphism in C#. Declaring a class does not create an object but defines how objects of that type will behave and what data they will hold.

```csharp
class Book
{
    public string Title;
    public string Author;
    public void Read()
    {
        Console.WriteLine("Reading book");
    }
}
```
---

## Q12: What is the relationship between a class and an object?
A class is the definition or blueprint; an object is an instance of that blueprint. You define structure and behavior in a class, and create actual usable data structures in memory (objects) based on that class. Multiple objects can be created from the same class, each with its own state. Classes serve as templates, while objects are actual implementations that make use of class definitions.

```csharp
class Cat
{
    public string Name;
}
Cat cat1 = new Cat();
Cat cat2 = new Cat();
cat1.Name = "Tom";
cat2.Name = "Jerry";
```
---

## Q13: Explain the basic features of OOPs
The basic features of OOP are:
1. **Encapsulation**: Bundling data and operations within objects and restricting access to internal state.
2. **Abstraction**: Hiding complex implementation details and exposing only necessary interfaces.
3. **Inheritance**: Acquiring properties and behaviors from other classes.
4. **Polymorphism**: Using one interface to represent multiple types or behaviors.

These features promote code reusability, flexibility, modularity, and a closer representation of real-world concepts.

```csharp
class Vehicle // Inheritance
{
    public virtual void Move() // Polymorphism
    {
        Console.WriteLine("Vehicle moves");
    }
}
class Bike : Vehicle
{
    public override void Move()
    {
        Console.WriteLine("Bike moves");
    }
}
```
---

## Q14: Can you specify the accessibility modifier for methods inside the interface?
No, in C# all members of an interface are implicitly public and abstract. You cannot specify any other accessibility modifier (private, protected, internal) for methods inside an interface. The implementation of those methods in a class can have different accessibility if implemented explicitly, but the interface itself requires that members are public.

```csharp
interface ILogger
{
    void Log(string message); // Implicitly public, cannot specify 'private void Log()'
}
```
---

# Mid

## Q15: Is it possible for a class to inherit the constructor of its base class?
No, constructors are not inherited in C#. The derived class does not have access to the base class’s constructors directly. However, derived classes can call a specific constructor of the base class using the base keyword, especially in their own constructors. This enables them to leverage initialization logic from the base class, but they must always define their own constructors explicitly.

```csharp
class Base
{
    public Base(int x) { }
}
class Derived : Base
{
    public Derived(int y) : base(y) // Calls Base(int)
    {
    }
}
```
---

## Q16: How could you define Abstraction in OOP?

Abstraction in OOP (Object-Oriented Programming) is the process of hiding the internal implementation details of a class and exposing only the relevant functionality to the user. It allows you to focus on what an object does instead of how it does it. Abstraction is typically achieved in C# using abstract classes and interfaces. These constructs define a contract or blueprint, while actual implementation happens in derived classes. By using abstraction, software becomes easier to extend and maintain. It helps to manage complexity by breaking down a program into smaller, well-defined pieces. In real applications, abstraction is often used to define system interfaces without specifying the low-level mechanics.

```csharp
// Abstract class providing abstraction
abstract class Animal
{
    public abstract void MakeSound();
}

// Concrete class providing implementation
class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Bark");
    }
}
```
---

## Q17: State the features of an Interface

An interface in C# defines a contract that implementing classes must adhere to. It can only contain declarations of methods, properties, events, or indexers, but no implementation. Interfaces cannot include fields, constructors, or destructors. A class or struct can implement multiple interfaces, supporting multiple inheritance in a limited way. All members of an interface are by default public and abstract (unless they are static or have default implementation from C# 8.0). Implementing an interface enforces certain behaviors across multiple classes, ensuring consistency. Interfaces are used for dependency injection and enable loosely coupled architectures.

```csharp
interface IPrintable
{
    void Print();
}

class Document : IPrintable
{
    public void Print()
    {
        Console.WriteLine("Printing Document");
    }
}
```
---

## Q18: What do you mean by Data Encapsulation?

Data Encapsulation is the OOP principle of bundling the data (fields) and methods (functions) that operate on the data into a single unit known as a class. It restricts direct access to some of the object's components, usually by making fields private and providing public getter and setter methods to control access. This ensures that the internal representation of the object is hidden from the outside. Encapsulation helps prevent the unintended modification of data, increases modularity, and allows validation or logic to be added easily.

```csharp
class Person
{
    private string name;

    public string Name
    {
        get { return name; }
        set { name = value; }
    }
}
```
---

## Q19: What are similarities between a class and a structure?

In C#, both classes and structures can have fields, methods, properties, events, and constructors. Both support implementing interfaces and both can be instantiated. You can define access modifiers like public, private, etc., with both. Both support parameterized constructors and can have static members. They allow the grouping of related data and behavior into a single unit. However, unlike classes, structures are value types, and classes are reference types.

```csharp
struct StructExample
{
    public int X;
    public void Display() { }
}

class ClassExample
{
    public int X;
    public void Display() { }
}
```
---

## Q20: Interface or an Abstract class: which one to use?

Use an interface when you need to define a contract that multiple unrelated classes can implement, or when you need to support multiple inheritance. Use an abstract class when you want to share base functionality among closely related classes and provide some common implementation along with abstract (unimplemented) members. If you require constructors, fields, or default behavior, choose an abstract class. If you only need to define signatures or contracts, use an interface. Note, in some cases, a combination of both can offer flexible architecture.

```csharp
interface IShape
{
    double GetArea();
}

abstract class Shape
{
    public abstract double GetArea();
    public void Display() { Console.WriteLine("I am a shape."); }
}
```
---

## Q21: How is method overriding different from method overloading?

Method overriding occurs when a child class redefines a method from its parent class using the same name, return type, and parameters, typically using the "override" keyword. It is used for runtime polymorphism. Method overloading happens within the same class and involves defining multiple methods with the same name but different signatures (parameter types, number, or order). Overloading is a form of compile-time polymorphism.

```csharp
// Overloading
class Sample
{
    public void DoWork() { }
    public void DoWork(int x) { }
}

// Overriding
class Base
{
    public virtual void Display() { }
}

class Derived : Base
{
    public override void Display() { Console.WriteLine("Derived"); }
}
```
---

## Q22: What is Unit Of Work?

Unit of Work is a design pattern used to group one or more operations (such as database updates) into a single transaction. It keeps track of changes to entities and ensures that all changes are committed or rolled back as a unit. This approach prevents data inconsistencies and reduces database round-trips. In .NET, Unit of Work is often used alongside the Repository pattern in data access layers, such as in Entity Framework’s DbContext, which tracks changes and saves them in a single transaction.

```csharp
public interface IUnitOfWork
{
    void Commit();
}

public class UnitOfWork : IUnitOfWork
{
    public void Commit()
    {
        // Commit logic, e.g., context.SaveChanges();
    }
}
```
---

## Q23: What are the different ways a method can be Overloaded?

A method can be overloaded by changing the number, type, or order of its parameters in the same class. You cannot overload by changing only the return type. Overloading allows one method name to perform different tasks based on input arguments. Static, instance, and constructors can be overloaded. It enhances code readability and flexibility.

```csharp
class Calculator
{
    public int Add(int a, int b) { return a + b; }
    public double Add(double a, double b) { return a + b; }
    public int Add(int a, int b, int c) { return a + b + c; }
}
```
---

## Q24: What's the difference between a method and a function in OOP context?

In OOP, a function is a block of code that performs a task, while a method is a function associated with a class or object. In C# specifically, all functions defined inside classes are called methods. Methods have access to class data (fields/properties), whereas a function may exist independently in some languages (not C#). Therefore, in C#, method and function are often used interchangeably, but formally, class-bound routines are methods.

```csharp
class MathOps
{
    public int Square(int x)
    {
        return x * x; // This is a method.
    }
}

// No standalone functions in C#, all inside classes.
```
---

## Q25: How can you prevent your class to be inherited further?

In C#, you can prevent a class from being inherited by marking it as sealed. A sealed class cannot be inherited by any other class. This is useful when you want to restrict further specialization or modification of behavior.

```csharp
sealed class FinalClass
{
    public void Show() { }
}

// class Derived : FinalClass {} // Error: cannot derive from sealed class
```
---

## Q26: What is the difference between Virtual method and Abstract method?

A virtual method in a base class provides a default implementation, which can optionally be overridden by derived classes. An abstract method, on the other hand, has no implementation in the base class and must be overridden in any non-abstract derived class. Abstract methods can only be declared in abstract classes, while virtual methods can be declared in regular or abstract classes.

```csharp
abstract class Base
{
    public virtual void VirtualMethod() { Console.WriteLine("Base implementation"); }
    public abstract void AbstractMethod();
}

class Derived : Base
{
    public override void VirtualMethod() { Console.WriteLine("Derived implementation"); }
    public override void AbstractMethod() { Console.WriteLine("Implemented"); }
}
```
---

## Q27: What is the difference between Interface and Abstract Class?

An interface only declares members without implementation (until C# 8.0, which allows default implementation), can't have fields, and supports multiple inheritance. An abstract class can have both abstract members (without implementation) and concrete members (with implementation), as well as fields, constructors, and destructors. Only single inheritance is supported for abstract classes. Use interfaces for capability contracts and abstract classes for shared base functionality.

```csharp
interface IExample
{
    void DoWork();
}

abstract class AbstractExample
{
    public abstract void DoWork();
    public void Helper() { }
}
```
---

## Q28: What is Polymorphism, what is it for, and how is it used?

Polymorphism means "many forms." It allows one interface to be used for a general class of actions. In C#, there are compile-time (method overloading) and runtime (method overriding) polymorphism. It enables you to write flexible and maintainable code, letting you use base class references to refer to derived class objects and invoke their overridden methods. Polymorphism is used extensively in frameworks, architecture, and design patterns to generalize code and promote extensibility.

```csharp
class Animal
{
    public virtual void Speak() { Console.WriteLine("Animal speaks"); }
}

class Cat : Animal
{
    public override void Speak() { Console.WriteLine("Meow"); }
}

Animal myAnimal = new Cat();
myAnimal.Speak(); // Output: Meow
```
---

## Q29: What are abstract classes? What are the distinct characteristics of an abstract class?

Abstract classes are base classes that cannot be instantiated directly. They can include abstract methods (no implementation) and regular methods (with implementation). Abstract classes provide a common definition for derived classes and force implementation of abstract members. They can have constructors, fields, properties, events, and access modifiers. Abstract classes are used when you want to provide some shared code along with the contract for further implementation in subclasses.

```csharp
abstract class Vehicle
{
    public abstract void Drive();
    public void Refuel() { Console.WriteLine("Vehicle refueled"); }
}

class Car : Vehicle
{
    public override void Drive() { Console.WriteLine("Driving Car"); }
}
```
---

## Q30: How can you prevent a class from overriding in C#?

To prevent a class’s method from being overridden further, mark the method as sealed in a derived class. The sealed modifier can only be used with override methods. If you want to prevent the entire class from being inherited, use the sealed keyword with the class itself.

```csharp
class Base
{
    public virtual void Show() { }
}

class Derived : Base
{
    public sealed override void Show() { }
}

// class MoreDerived : Derived
// {
//     public override void Show() { } // Error: cannot override sealed method
// }
```
---

# Senior

## Q31: When should I use a struct instead of a class?

A struct in C# should be used instead of a class when you need a lightweight object that represents a single value or a small collection of related values. Structs are value types, meaning they are stored on the stack and copied by value, not by reference. This makes them ideal for small, short-lived objects that do not require inheritance or reference semantics. Use structs when immutability, performance, and memory consumption are priorities—for example, for points, vectors, complex numbers, or color representations. However, structs cannot have default constructors, inherit from another struct/class, or be the base of another type. Avoid using structs for large objects or those that require polymorphism, deep copy, or reference sharing.

```csharp
public struct Point
{
    public int X;
    public int Y;
}

Point a = new Point { X = 1, Y = 2 };
Point b = a;
b.X = 5; // Does not affect a.X because structs are copied by value
```
---

## Q32: Explain the concept of Destructor

A destructor in C# is a special method invoked just before an object is destroyed by the garbage collector. It is used to perform cleanup operations, such as releasing unmanaged resources (e.g., file handles, database connections) that are not handled by the .NET garbage collector. A destructor is declared using a tilde (~) followed by the class name and cannot have parameters or access modifiers. Destructors cannot be called explicitly or inherited, and they cannot be overloaded. They are typically unnecessary unless your class holds unmanaged resources. In most cases, you should implement the `IDisposable` interface and use the `Dispose` pattern for deterministic cleanup, as destructor timing is non-deterministic.

```csharp
class FileHolder
{
    ~FileHolder()
    {
        // Clean up resources
    }
}
```
---

## Q33: How to solve Circular Reference?

Circular reference occurs when two or more objects reference each other, potentially causing memory leaks, stack overflow, or serialization problems. Common solutions include refactoring relationships using interfaces or weak references, removing unnecessary dependencies, or breaking the cycle with design patterns (like event aggregators). You can use dependency injection, composition, or observer patterns to decouple objects. In serialization, you might use attributes (e.g., `[JsonIgnore]`) to prevent infinite loops. Proper architecture and well-designed object ownership avoid circular references.

```csharp
class A
{
    public B ReferenceToB { get; set; }
}

class B
{
    public A ReferenceToA { get; set; }
}

// Remove one side or use interface to decouple
```
---

## Q34: Could you explain some benefits of Repository Pattern?

The Repository Pattern abstracts the data layer, providing a central interface for data access. Its main benefits include decoupling the domain and data mapping layers, enabling unit testing by mocking repositories, promoting single responsibility and separation of concerns, and centralizing data logic. It simplifies code maintenance and change by isolating database logic, supports switching data sources with minimal client impact, and can enforce business rules. The pattern makes code cleaner and easier to understand, especially for large projects with complex persistence logic.

```csharp
public interface ICustomerRepository
{
    Customer GetById(int id);
    void Add(Customer customer);
}

public class CustomerRepository : ICustomerRepository
{
    // Implementation of data access
}
```
---

## Q35: What is Coupling in OOP?

Coupling describes how closely connected different classes or modules are. Tight coupling means classes know too much about each other, making the system rigid, difficult to modify, or test. Loose coupling limits dependencies and promotes flexibility, maintainability, and testability. Reducing coupling is often achieved through interfaces, dependency injection, and design patterns like Factory or Observer. Lower coupling allows for easier refactoring and component replacement and minimizes side effects. Good object-oriented design strives for loose coupling and high cohesion to create robust codebases.

```csharp
public interface IMessageSender
{
    void Send(string message);
}

public class EmailSender : IMessageSender
{
    public void Send(string message) { /* ... */ }
}

public class NotificationService
{
    private IMessageSender _sender;
    public NotificationService(IMessageSender sender)
    {
        _sender = sender;
    }
}
```
---

## Q36: What exactly is the difference between an Interface and abstract class?

An interface defines a contract of method/property signatures without implementation, while an abstract class provides a partial implementation and can contain fields, properties, and methods (including some with code). A class can implement multiple interfaces but inherit from only one abstract class. Interfaces cannot have access modifiers on members (public by default) and cannot store state, whereas abstract classes can have constructors, fields, and non-abstract members. Abstract classes are used for sharing code among closely related types, while interfaces express capability (e.g., "can be compared") and support polymorphic behavior across unrelated types.

```csharp
public interface IFlyable
{
    void Fly();
}

public abstract class Bird
{
    public abstract void Sing();
    public void Eat() { /* default implementation */ }
}
```
---

## Q37: Explain different types of Inheritance

OOP supports several types of inheritance: 
- Single inheritance (a class inherits from one base)
- Multiple inheritance (a class inherits from more than one base, not supported for classes in C#, but can be achieved via interfaces)
- Multilevel inheritance (a class derives from another derived class)
- Hierarchical inheritance (multiple classes inherit from one base)
- Hybrid inheritance (combination, but can lead to complications, so interfaces are often favored in C#)
C# allows single, multilevel, hierarchical inheritance via classes and multiple/ hybrid inheritance through interfaces.

```csharp
// Single
class Animal {}
class Dog : Animal {}

// Hierarchical
class Cat : Animal {}

// Multilevel
class Puppy : Dog {}

// Multiple via interface
interface IRunner { void Run(); }
interface IJumper { void Jump(); }
class Athlete : IRunner, IJumper
{
    public void Run() { }
    public void Jump() { }
}
```
---

## Q38: What's the advantage of using getters and setters - that only get and set - instead of simply using public fields for those variables?

Using getters and setters (properties) instead of public fields encapsulates fields, enabling you to add logic (validation, logging) later without breaking changes or exposing implementation. Properties provide more control over data access, allow read-only or write-only states, and enable data binding and serialization support. Refactoring or modifying property logic is safer for public APIs; public fields limit maintainability and testability. Encapsulation through properties is fundamental for robust, scalable designs.

```csharp
public class Person
{
    private int age;
    public int Age
    {
        get { return age; }
        set { age = value; }
    }
}
```
---

## Q39: Differentiate between an abstract class and an interface

Abstract classes can provide both abstract (no implementation) and concrete (with implementation) members; interfaces only define signatures. Abstract classes can define constructors, fields, and retain state, while interfaces cannot. A class can inherit only one abstract class but implement multiple interfaces. Abstract classes are ideal for closely related objects with shared logic; interfaces are for defining capabilities across unrelated classes, enabling polymorphism. Starting from C# 8.0, interfaces can have default implementations (but still can't hold state), further narrowing this gap but not eliminating key differences.

```csharp
public abstract class Vehicle
{
    public abstract void Drive();
    public void Refuel() { /* implementation */ }
}

public interface IDriveable
{
    void Drive();
}
```
---

## Q40: What is a static constructor?

A static constructor is a special constructor used to initialize static members of a class. It is called automatically before the first instance is created or any static members are referenced. You cannot call it directly, specify parameters, or have access modifiers (always parameterless and without access qualifiers). It executes only once for the type, regardless of how many objects are created. Use static constructors to initialize static data or perform actions that need to occur only once.

```csharp
class Logger
{
    public static string DefaultPath;
    static Logger()
    {
        DefaultPath = "log.txt";
    }
}
```
---

## Q41: What is the difference between an abstract function and a virtual function?

An abstract function defines a method signature without implementation in an abstract class; derived classes must override it. A virtual function provides a default implementation but allows derived classes to override it. Abstract functions require the class to be abstract, while virtual functions don't. Abstract functions force implementation in derived classes, virtual functions offer it as optional but extendable behavior.

```csharp
public abstract class Animal
{
    public abstract void Speak(); // must be implemented
    public virtual void Eat() { Console.WriteLine("Eating"); } // can be overridden
}
```
---

## Q42: What is the difference between Cohesion and Coupling?

Cohesion describes how closely related the responsibilities of a single module/class are; high cohesion means a class does one well-defined thing. Coupling is about the degree of interdependence between modules/classes. High cohesion and low coupling are desired; high cohesion enables easier maintenance and testing, while loose coupling allows for independent changes across modules. Together, they improve software quality and adaptability to change.

```csharp
// High cohesion: Order class handles everything about Orders
public class Order
{
    public void CalculateTotal() { }
    public void SubmitOrder() { }
}

// Loose coupling via interface
public interface INotifier { void Notify(string message); }
```
---

## Q43: When should I use an Interface and when should I use a Base Class?

Use an interface to define a contract for unrelated classes or provide multiple capability implementations (since classes can implement multiple interfaces). Use a base class to share code and provide a foundation for closely related classes with common logic, enforcing a single inheritance chain. If you need shared implementation, state, or constructors, use a base class; if you need polymorphic behavior across different class hierarchies, use interfaces. In some cases, both can be combined for maximum flexibility.

```csharp
interface IFlyable { void Fly(); } // capability

abstract class Animal
{
    public void Eat() { }
    public abstract void MakeSound();
}
```
---

## Q44: What is Cohesion in OOP?

Cohesion refers to how focused the responsibilities of a class or module are. High cohesion means a class has a single, well-defined responsibility, promoting maintainability, testability, and reusability. Low cohesion indicates a class is handling multiple unrelated tasks, leading to complexity and making it harder to update or debug. Good OOP design favors high cohesion, where each module encapsulates only related behavior or data, following principles like Single Responsibility Principle.

```csharp
public class CustomerRepository
{
    public void AddCustomer(Customer customer) { }
    public Customer GetCustomer(int id) { }
}
// Only customer operations: High cohesion
```
---

## Q45: Can you declare an overridden method to be static if the original method is not static?

No, in C# you cannot declare an overridden method as static if the original method is not static. Method overriding requires the method signatures in the base and derived classes to match exactly, including the static modifier. Static methods belong to the type itself, not instances, and cannot be virtual, abstract, or overridden. Only instance methods can participate in inheritance-based polymorphism through overriding; static methods can be hidden using the `new` keyword, but not overridden.

```csharp
class Base
{
    public virtual void Show() { }
}

class Derived : Base
{
    // This will not compile:
    // public static override void Show() { }

    // You can hide a static method, but not override:
    public new static void Show() { }
}
```
---

## Q46: Does .NET support Multiple Inheritance?

.NET does not support multiple inheritance for classes. This means a class cannot inherit from more than one base class—each class has a single direct parent. The reason behind this is to avoid ambiguity, such as the "diamond problem," where a class might inherit the same member from multiple paths. However, .NET does allow a class to implement multiple interfaces, which enables a form of multiple inheritance of type. Interfaces only define contracts (methods, properties, events, etc.) without implementation, so there's no ambiguity or conflict with implementation details. This strikes a balance between flexibility and safety in object models. If you need behaviors from multiple sources, you can use interfaces or composition patterns instead of multiple class inheritance.

```csharp
interface IFly
{
    void Fly();
}

interface ISwim
{
    void Swim();
}

class Duck : IFly, ISwim
{
    public void Fly()
    {
        // Implement flying
    }

    public void Swim()
    {
        // Implement swimming
    }
}

// Invalid: multiple base classes are not allowed
// class Example : ClassA, ClassB { } // Error!
```
---

# Expert

## Q47: Why prefer Composition over Inheritance? What trade-offs are there for each approach? When should you choose Inheritance over Composition?

Composition is generally preferred over inheritance because it promotes flexibility, reduces tight coupling, and allows for components to be reused in different contexts. In composition, you build complex objects by combining simpler objects, leading to more maintainable and extensible designs. Inheritance, on the other hand, tightly couples a derived class to a base class, often resulting in rigid structures and unwanted side effects if the base class changes. Composition favors code reuse through has-a relationships, while inheritance uses is-a relationships. Use inheritance when defining a clear hierarchical relationship and base behaviors, and use composition when you want to combine behaviors dynamically or avoid inheriting unwanted properties. The trade-offs are that inheritance simplifies code when you naturally have a strict taxonomy but can lead to fragile bases; composition requires more delegation but gives greater flexibility.

```csharp
class Engine
{
    public void Start() { }
}

class Car
{
    private Engine engine = new Engine();

    public void StartCar()
    {
        engine.Start();
    }
}

// Inheritance (less flexible in changing behavior at runtime)
class Animal { }
class Dog : Animal { }
```
---

## Q48: Could you elaborate Polymorphism vs Overriding vs Overloading?

Polymorphism enables a single interface to represent different data types or classes, allowing one piece of code to operate on multiple types seamlessly. Overriding is the process where a derived class provides its own implementation of a method defined in the base class, enabled via the virtual/override keywords—this is an aspect of runtime (dynamic) polymorphism. Overloading, by contrast, occurs when multiple methods in the same scope have the same name but different parameter lists (types or count); this is resolved at compile time. Polymorphism provides flexibility and extensibility in code, overriding customizes inherited functionality, and overloading improves code readability and usability. 

```csharp
class Animal
{
    public virtual void Speak() { Console.WriteLine("Animal speaks"); }
}

class Dog : Animal
{
    public override void Speak() { Console.WriteLine("Dog barks"); }
}

class Calculator
{
    public int Add(int a, int b) { return a + b; }
    public double Add(double a, double b) { return a + b; } // Overloaded
}
```
---

## Q49: What is LSP (Liskov Substitution Principle) and what are some examples of its use (good and bad)?

Liskov Substitution Principle (LSP) states that objects of a derived class must be substitutable for objects of the base class without altering the desirable properties of the program (correctness, tasks performed). In simpler terms, if a class S is a subclass of class T, then objects of type T should be replaceable with objects of type S without breaking the program. Good LSP adherence ensures inheritance hierarchies are logical and maintainable. A bad example is a Square class inheriting from a Rectangle—setting width separately from height in Rectangle works, but not for Square, which violates expectations. Good use is Dog inheriting from Animal, where all behaviors and expectations are preserved.

```csharp
class Rectangle
{
    public virtual int Width { get; set; }
    public virtual int Height { get; set; }
}

class Square : Rectangle  // Violates LSP
{
    public override int Width { set { base.Width = base.Height = value; } }
    public override int Height { set { base.Width = base.Height = value; } }
}

// Good example:
class Animal
{
    public virtual void Speak() { }
}

class Dog : Animal
{
    public override void Speak() { Console.WriteLine("Bark"); }
}
```
---

## Q50: You have defined a destructor in a class that you have developed by using the C#, but the destructor never executed. Why?

In C#, destructors (finalizers) are not guaranteed to execute immediately when an object goes out of scope because .NET uses a garbage collector to manage memory. Finalizers run only when the GC collects the object, which might never happen if the app is short-lived or forced termination occurs before collection. Also, GC is non-deterministic; you can't predict exactly when (or even if) the destructor will be called. This is why critical cleanup tasks should be placed in Dispose (by implementing IDisposable) rather than relying solely on destructors. Relying on destructors for timely resource cleanup leads to unpredictable behavior and resource leaks.

```csharp
class MyClass
{
    ~MyClass()
    {
        Console.WriteLine("Destructor called");
    }
}

// Use IDisposable for deterministic cleanup
class SafeResource : IDisposable
{
    public void Dispose()
    {
        Console.WriteLine("Disposed");
    }
}
```
---

## Q51: Can you declare a private class in a namespace?

No, you cannot declare a private class at the namespace level in C#. Namespace-level types (classes, interfaces, structs) can only have public or internal accessibility. The private modifier is only allowed for nested types (classes declared within another class or struct). This is because private members are for hiding implementation details within the enclosing type, not across a namespace, ensuring clarity and maintainability of code.

```csharp
// Invalid:
// private class MyClass {} // Error!

// Valid:
internal class MyInternalClass {}

class Outer
{
    private class InnerClass { } // Nested private class, valid
}
```
---

## Q52: In terms that an OOP programmer would understand (without any functional programming background), what is a monad?

In simple OOP terms, a monad is a design pattern that wraps a value and provides a way to chain operations on that value while managing side-effects or context. It helps encapsulate behaviors like error handling, state, or async operations. A monad provides two essential operations: a way to wrap values into the monad (e.g., return) and a way to chain computations while preserving the context (e.g., bind). In C#, nullable types, tasks, and LINQ’s select/where chains are practical monad-like constructs. Monads can increase code safety and composability by abstracting repetitive patterns.

```csharp
// Nullable<T> works like a Maybe monad
int? value = 5;
int? result = value?.ToString().Length;

// LINQ's Select/SelectMany demonstrates monad chaining
var query = from x in new List<int> { 1, 2 }
            from y in new List<int> { 3, 4 }
            select x + y;
```
---

## Q53: What is the difference between Association, Aggregation and Composition?

These terms describe relationships between objects. Association is a general relationship where one object knows about another; for example, a teacher and a student. Aggregation is a special form of association representing a "has-a" relationship, where the lifetime of the parts is independent of the whole, e.g., a university and its students. Composition is a strong form of aggregation; the contained objects’ lifetimes are strictly tied to the container. If the containing object is destroyed, so are its parts, e.g., a house and its rooms. Understanding these relationships helps to design better and more maintainable systems.

```csharp
// Association
class Teacher
{
    public void SetStudent(Student s) { }
}

// Aggregation
class Department
{
    public List<Teacher> Teachers { get; set; }
}

// Composition
class House
{
    private Room room = new Room();
}
```
---

## Q54: What is the difference between a Mixin and Inheritance?

A mixin is a pattern that lets you compose classes from reusable pieces of behavior, typically through interfaces combined with extension methods or partial classes in C#. Inheritance, on the other hand, creates an explicit parent-child relationship. Multiple mixins can be applied to one class, adding capabilities without forming a hierarchical relationship, while inheritance is strictly is-a and single-parent in C#. Mixins promote code reuse and modularity by allowing classes to pick and choose behaviors, avoiding the tight coupling and limitations of deep inheritance chains.

```csharp
interface ILogger
{
    void Log(string message);
}

static class LoggerMixin
{
    public static void Log(this ILogger obj, string message)
    {
        Console.WriteLine(message);
    }
}

class MyClass : ILogger {}
```
---

## Q55: What does it mean to Program to an Interface?

Programming to an interface means writing code that depends on abstractions (interfaces) rather than concrete implementations. This principle increases flexibility, maintainability, and testability, as you can easily swap implementations without changing client code. It aligns with the Dependency Inversion Principle from SOLID and promotes loose coupling—your code relies only on what an object can do, not how it does it. In .NET, interfaces are used to define contracts that different classes may follow, making code more modular and flexible to changes.

```csharp
interface IRepository
{
    void Add(object item);
}

class SqlRepository : IRepository
{
    public void Add(object item)
    {
        // Add to SQL database
    }
}

void SaveItem(IRepository repo, object item)
{
    repo.Add(item); // Works for any implementation of IRepository
}
```
---

## Q56: Can you provide a simple explanation of methods vs. functions in OOP context?

In OOP, a method is a function associated with an object or class—it is a member function that operates on instance data or class-level data. A function is a general term for any subroutine that takes inputs, performs a task, and returns a result (if any). In C#, free-standing functions cannot exist; all functions are defined as methods within a class or struct. Thus, in C#, method and function are often used interchangeably, but method emphasizes their relationship to an object/class.

```csharp
class Calculator
{
    // Method (also a function)
    public int Add(int a, int b)
    {
        return a + b;
    }
}
```
---

## Q57: Why doesn't C# allow static methods to implement an interface?

C# doesn't allow static methods to implement an interface because interfaces define a contract for instance members; they expect behaviors that can be invoked on an instance of a class, not the class itself. Static members belong to the type and not to any object instance, making it incompatible with interfaces, whose main purpose is to provide polymorphism. Instance methods can be overridden and can participate in interfaces’ polymorphic behavior, but static methods cannot. This design ensures interface contracts are focused on instance-based operations, promoting consistency and predictability.

```csharp
interface IFoo
{
    void DoSomething(); // Instance member
}

// Not allowed:
// static void DoSomething(); // Interfaces cannot have static methods
``` 
---