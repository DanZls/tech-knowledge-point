# Entry

## Q1: What are the main categories of Design Patterns?
Design patterns are typically divided into three main categories:

1. **Creational Patterns**: These focus on object creation mechanisms, trying to create objects in a manner suitable to the situation. Examples: Singleton, Factory, Abstract Factory, Builder, Prototype.
2. **Structural Patterns**: These deal with object composition, forming large structures from individual objects. Examples: Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy.
3. **Behavioral Patterns**: These focus on communication between objects, what goes on between objects and how responsibilities are assigned. Examples: Observer, Mediator, Command, Iterator, State, Strategy, Template, Chain of Responsibility, Memento, Interpreter, Visitor.

This categorization helps developers easily select the right pattern for a specific problem domain.

```csharp
// Example of pattern types:
class Singleton { }
class Adapter { }
class Observer { }
```
---

## Q2: What is Design Patterns and why anyone should use them?
Design patterns are proven, reusable solutions to common problems in software design. They offer templates for how to solve specific problems in coding and architecture, making code more flexible, maintainable, and scalable. Developers use them to avoid reinventing the wheel and to communicate design approaches more efficiently with other developers. Patterns also help ensure best practices are followed, resulting in fewer bugs and improved code quality. Over time, design patterns have become a common vocabulary for architects and engineers.

```csharp
// Pattern example: Singleton
public class Logger
{
    private static Logger instance;
    private Logger() {}
    public static Logger Instance => instance ??= new Logger();
}
```
---

## Q3: What is Singleton pattern?
The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. This is useful when exactly one object is needed to coordinate actions across a system, like a configuration manager or logger. The pattern restricts instantiation of the class and provides a static method for retrieval. It's important to handle thread safety when implementing Singleton in multithreaded applications. However, excessive use of Singleton can lead to hidden dependencies and make unit testing difficult.

```csharp
public class Singleton
{
    private static Singleton instance;
    private static readonly object lockObj = new object();
    private Singleton() { }
    public static Singleton Instance
    {
        get
        {
            lock (lockObj)
            {
                return instance ??= new Singleton();
            }
        }
    }
}
```
---

## Q4: What is a pattern?
A pattern in software design refers to a reusable and general solution to a commonly occurring problem within a given context. It provides a blueprint for solving the problem but is not code itself; rather, it describes the structure and interaction of classes or objects. Patterns can be applied repeatedly throughout the design and development of software. Using patterns improves communication among developers and results in more robust and flexible codebases.

```csharp
// An example design pattern blueprint; does not have to be code-specific.
public interface Pattern { void Apply(); }
```
---

# Junior

## Q5: Why would you want to use a Repository Pattern with an ORM?
Using the Repository Pattern with an ORM (Object-Relational Mapper) abstracts the data access layer, providing a clean API for the application to interact with data sources. It allows you to decouple business logic from database queries, making the system easier to test and maintain. With repositories, you can swap ORMs or underlying data sources without changing business logic. It also centralizes data logic and provides better control over data retrieval and storage.

```csharp
public interface ICustomerRepository
{
    Customer GetById(int id);
    void Add(Customer customer);
}
public class CustomerRepository : ICustomerRepository
{
    private readonly DbContext context;
    public CustomerRepository(DbContext context) { this.context = context; }
    public Customer GetById(int id) => context.Customers.Find(id);
    public void Add(Customer customer) => context.Customers.Add(customer);
}
```
---

## Q6: What are some benefits of Repository Pattern?
The Repository Pattern provides several benefits:
- Decouples business logic from data access logic.
- Centralizes data access functionality, making code more maintainable and testable.
- Simplifies mocking data access during unit testing.
- Allows easy swapping of data sources (e.g., switching from SQL Server to MongoDB).
- Encourages a clean, domain-driven design by exposing only what the domain needs, not the database implementation.
- Supports the Single Responsibility Principle.

```csharp
public interface IProductRepository
{
    IEnumerable<Product> GetAll();
}
public class ProductRepository : IProductRepository
{
    public IEnumerable<Product> GetAll() => ...; // Data access logic
}
```
---

## Q7: Name types of Design Patterns?
The main types (categories) of design patterns are:
1. **Creational**: e.g., Singleton, Factory, Builder, Abstract Factory, Prototype.
2. **Structural**: e.g., Adapter, Decorator, Composite, Proxy, Bridge, Facade, Flyweight.
3. **Behavioral**: e.g., Strategy, Observer, Command, State, Template Method, Iterator, Chain of Responsibility, Mediator, Memento, Interpreter, Visitor.

```csharp
// Creational: Factory, Structural: Adapter, Behavioral: Observer
```
---

## Q8: What is Null Object pattern?
The Null Object Pattern provides an object as a surrogate for the lack of an object. Rather than using `null` references which can lead to `NullReferenceException` errors, the pattern supplies a default object that adheres to the expected interface but performs no operation. This approach simplifies code by not requiring repeated null checks and can improve code readability and reliability.

```csharp
public interface ILogger
{
    void Log(string message);
}
public class NullLogger : ILogger
{
    public void Log(string message) { /* Do nothing */ }
}
```
---

## Q9: What is Dependency Injection?
Dependency Injection (DI) is a design pattern that handles the dependencies of a class from the outside, rather than the class creating its dependencies itself. This enhances testability, flexibility, and maintainability by promoting loose coupling between classes. There are several types of DI—constructor injection, property injection, and method injection. In .NET, DI is commonly supported by frameworks like ASP.NET Core’s built-in container.

```csharp
public class ProductService
{
    private readonly IProductRepository repo;
    public ProductService(IProductRepository repo) { this.repo = repo; }
}
```
---

## Q10: What is Proxy pattern?
The Proxy pattern provides an object that acts as a surrogate or placeholder for another object to control access to it. It can handle extra functionality like lazy initialization, access control, logging, or caching without changing the original object's code. Common proxy types are virtual, protection, and remote proxies.

```csharp
public interface IImage { 
    void Display(); 
}
public class ImageProxy : IImage
{
    private RealImage realImage;
    public void Display()
    {
        realImage ??= new RealImage();
        realImage.Display();
    }
}
```
---

## Q11: What is Inversion of Control?
Inversion of Control (IoC) is a principle whereby the control of object creation and dependency management is transferred from the class itself to an external entity or framework. Instead of a class instantiating its dependencies, they are provided externally (often through DI containers). IoC leads to flexible, loosely coupled, and testable code.

```csharp
// Instead of: var repo = new ProductRepository();
// Use IoC: IProductRepository repo = container.Resolve<IProductRepository>();
```
---

## Q12: What is Iterator pattern?
The Iterator Pattern provides a way to sequentially access elements of a collection without exposing its underlying representation. This allows a standardized way to traverse collections, enabling flexibility in how internal data structures are implemented.

```csharp
public interface IIterator<T>
{
    bool HasNext();
    T Next();
}
public class ListIterator<T> : IIterator<T>
{
    private readonly List<T> items;
    private int index;
    public ListIterator(List<T> items) { this.items = items; }
    public bool HasNext() => index < items.Count;
    public T Next() => items[index++];
}
```
---

## Q13: What is State pattern?
The State pattern allows an object to alter its behavior when its internal state changes. In practice, it encapsulates the behavior associated with a particular state into separate classes and delegates state-specific behavior to the current state object. This promotes the Open/Closed Principle and can simplify complex conditional logic.

```csharp
public interface IState { 
    void Handle(Context context); 
}
public class Context
{
    public IState State { get; set; }
    public void Request() => State.Handle(this);
}
public class StartState : IState
{
    public void Handle(Context context) { /* Do something and change state */ }
}
```
---

## Q14: What is Template pattern?
The Template (Template Method) pattern defines the skeleton of an algorithm in a base class, deferring some implementation steps to subclasses. This allows shared logic to reside in one place while subclasses can customize certain behaviors, promoting code reuse and consistency.

```csharp
public abstract class DataParser
{
    public void Parse() {
        ReadData();
        ProcessData();
        SaveData();
    }
    protected abstract void ReadData();
    protected abstract void ProcessData();
    protected abstract void SaveData();
}
```
---

## Q15: What is Filter pattern?
The Filter (Criteria) Pattern allows filtering of collections of objects using different criteria and combining them in a decoupled, flexible way. Criteria can be reused and combined using logical operations like AND/OR, improving the maintainability and extensibility of filtering logic.

```csharp
public interface ICriteria<T>
{
    IEnumerable<T> MeetCriteria(IEnumerable<T> items);
}
public class AdultCriteria : ICriteria<Person>
{
    public IEnumerable<Person> MeetCriteria(IEnumerable<Person> items)
        => items.Where(p => p.Age >= 18);
}
```
---

## Q16: What is Builder pattern?
The Builder Pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations. It’s useful when an object requires multiple steps to create or when some parameters are optional.

```csharp
public class Car { 
    public string Engine; 
    public int Seats; 
}
public class CarBuilder
{
    private readonly Car car = new Car();
    public CarBuilder SetEngine(string engine) { 
        car.Engine = engine; 
        return this; 
    }
    public CarBuilder SetSeats(int seats) { 
        car.Seats = seats; 
        return this; 
    }
    public Car Build() => car;
}
```
---

## Q17: What is Strategy pattern?
The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. This pattern lets you change the algorithm independently from clients that use it, promoting the Open/Closed Principle and reducing code duplication.

```csharp
public interface ICompressionStrategy { 
    void Compress(string file); 
}
public class ZipCompression : ICompressionStrategy { 
    public void Compress(string file) { /*...*/ } 
}
public class Context
{
    public ICompressionStrategy Strategy { get; set; }
    public void CompressFile(string file) => Strategy.Compress(file);
}
```
---

## Q18: Can we create a clone of a singleton object?
No, a properly designed singleton class should not allow cloning, as doing so would break the guarantee of a single instance. However, if the singleton does not prevent cloning (e.g., it’s not sealed or doesn’t override the `MemberwiseClone` method), it’s technically possible, which is a design flaw. To prevent this, override clone methods and throw exceptions.

```csharp
public class Singleton
{
    private Singleton() { }
    public static Singleton Instance { get; } = new Singleton();
    protected Singleton Clone() { throw new NotSupportedException(); }
}
```
---

## Q19: What is Factory pattern?
The Factory Pattern defines an interface or method for creating objects, but lets subclasses (or factory methods) decide which class to instantiate. It encapsulates object creation, helping manage complexities, support extensibility, and adhere to the Single Responsibility Principle. The two main variations are the Simple Factory and Factory Method patterns.

```csharp
public interface IAnimal { 
    void Speak(); 
}
public class Dog : IAnimal { 
    public void Speak() => Console.WriteLine("Woof"); 
}
public class AnimalFactory
{
    public static IAnimal CreateAnimal(string type) => type == "dog" ? new Dog() : null;
}
```
---

# Mid

## Q20: Is Unit Of Work equals Transaction? Or it is more than that?
Unit of Work (UoW) is a design pattern that maintains a list of changes (inserts, updates, deletes) done in a business transaction and coordinates the writing of those changes to the database as a single unit. While it can use transactions to ensure atomicity, Unit of Work also tracks new, changed, and deleted objects and manages the complex orchestration of updates, making it more than just a database transaction. In other words, Transaction ensures all-or-nothing persistence; Unit of Work manages *what* should be persisted and coordinates it in batches. Most ORMs like Entity Framework implement Unit of Work internally, handling change tracking, identity maps and commit logic.

```csharp
public interface IUnitOfWork : IDisposable
{
    void Commit();
}
public class UnitOfWork : IUnitOfWork
{
    private readonly DbContext context;
    public UnitOfWork(DbContext context) { this.context = context; }
    public void Commit() { context.SaveChanges(); }
    public void Dispose() { context.Dispose(); }
}
```
---

## Q21: What is Decorator pattern?
The Decorator pattern allows you to add new behaviors or functionalities to objects dynamically without altering their structure. It achieves this by wrapping the original class with a new class that implements the same interface, then delegates calls to the original object, adding its own logic before or after forwarding the call. This pattern supports the Open/Closed Principle by allowing classes to be open for extension but closed for modification. In .NET, this is useful when you want to add responsibilities to individual objects, not to an entire class, as opposed to inheritance. Decorators can be stacked, enabling flexible composition of behaviors, such as logging or validation. This pattern is commonly used in stream classes (System.IO.Stream) and UI frameworks. The main benefit is increased flexibility and reduced class explosion compared to multiple subclassing.

```csharp
public interface IMessage
{
    string GetContent();
}

public class SimpleMessage : IMessage
{
    public string GetContent() => "Hello.";
}

// Decorator
public class EncryptedMessage : IMessage
{
    private IMessage _message;
    public EncryptedMessage(IMessage message) => _message = message;
    public string GetContent() => $"Encrypted({_message.GetContent()})";
}

// Usage
var message = new EncryptedMessage(new SimpleMessage());
Console.WriteLine(message.GetContent()); // Encrypted(Hello.)
```
---

## Q22: What is Memento pattern?
The Memento pattern is a behavioral design pattern that enables saving and restoring the previous state of an object without violating its encapsulation. The pattern involves three main participants: the Originator (whose state needs to be saved/restored), the Memento (an object storing the state), and the Caretaker (which requests saving/restoring but does not modify the state itself). It's useful for implementing undo/redo functionality, checkpoints, or history mechanisms in applications. By keeping the state between objects separated, you avoid leaking implementation details and can safely restore state as required. This pattern is commonly used in text editors, graphics editors, and other applications where state rollback is needed.

```csharp
// Originator
class Editor
{
    public string Content { get; set; }
    public Memento Save() => new Memento(Content);
    public void Restore(Memento memento) => Content = memento.Content;
}

class Memento
{
    public string Content { get; }
    public Memento(string content) => Content = content;
}

// Usage
var editor = new Editor { Content = "Version 1" };
var checkpoint = editor.Save();
editor.Content = "Version 2";
editor.Restore(checkpoint); // Content is "Version 1" again
```
---

## Q23: What is Unit Of Work?
Unit of Work is a design pattern that maintains a list of operations (such as insert, update, delete) to be performed during a business transaction and commits them all together, ensuring atomicity. In .NET applications, the Unit of Work pattern is often implemented alongside the Repository pattern to coordinate the work of multiple repositories under a single transaction. This pattern helps to avoid having partial updates in the event of errors and minimizes the number of database calls for performance. It encapsulates transaction management, change tracking, and concurrency, which reduces code duplication and ensures data consistency. Entity Framework’s DbContext is a built-in example of the Unit of Work pattern.

```csharp
public interface IUnitOfWork : IDisposable
{
    void Commit();
}

public class MyUnitOfWork : IUnitOfWork
{
    private readonly AppDbContext _context;
    public MyUnitOfWork(AppDbContext context) => _context = context;
    public void Commit() => _context.SaveChanges();
    public void Dispose() => _context.Dispose();
}
```
---

## Q24: What is Mediator pattern?
The Mediator pattern is a behavioral design pattern that encapsulates how a set of objects interact, promoting loosely coupled communication by keeping objects from referring to each other directly. Instead, they communicate through a mediator object. This pattern reduces dependencies between communicating objects, making the code easier to maintain and extend. In .NET, this approach is often seen in event-driven programming, UI frameworks, or with libraries like MediatR. By centralizing communication, the mediator enhances code reusability and testability.

```csharp
public interface IMediator
{
    void Notify(object sender, string ev);
}

public class ConcreteMediator : IMediator
{
    public UIControl1 Control1 { get; set; }
    public UIControl2 Control2 { get; set; }
    public void Notify(object sender, string ev)
    {
        if (ev == "Changed") { /* update another control */ }
    }
}

// Usage
var mediator = new ConcreteMediator();
mediator.Control1 = new UIControl1(mediator);
```
---

## Q25: What are some reasons to use Repository Pattern?
The Repository Pattern abstracts the data storage mechanism, providing a central point for data access logic. Using it helps enforce separation of concerns by decoupling business logic from data access code, which eases unit testing (by mocking repositories), promotes code reusability, and supports adherence to the Single Responsibility Principle. This pattern also allows changing the data source (e.g., switching from SQL Server to MongoDB) with minimal changes to higher layers of code. In domain-driven design, repositories represent collections of aggregate roots, hiding query complexity behind simple methods. They also help in keeping code clean, maintainable, and focused.

```csharp
public interface ICustomerRepository
{
    Customer GetById(int id);
    void Add(Customer customer);
}

public class CustomerRepository : ICustomerRepository
{
    private readonly DbContext _context;
    public CustomerRepository(DbContext context) => _context = context;
    public Customer GetById(int id) => _context.Customers.Find(id);
    public void Add(Customer customer) => _context.Customers.Add(customer);
}
```
---

## Q26: What is an Aggregate Root in the context of Repository Pattern?
An Aggregate Root is an entity within a domain model that acts as the main entry point for a particular aggregate—a group of related entities treated as a unit for data changes. Only the aggregate root can be retrieved or saved via a repository, enforcing encapsulation and data consistency by preventing external objects from directly referencing or manipulating child entities. By modeling data in terms of aggregates and aggregate roots, you define transactional boundaries and promote consistency. Aggregate Roots are a critical concept in Domain-Driven Design.

```csharp
public class Order // Aggregate Root
{
    public int Id { get; set; }
    public List<OrderItem> Items { get; set; } = new();
    public void AddItem(OrderItem item) => Items.Add(item);
}

public class OrderItem // Child entity
{
    public int ProductId { get; set; }
    public int Quantity { get; set; }
}
```
---

## Q27: Can you give any good explanation what is the difference between Proxy and Decorator?
Both Proxy and Decorator patterns use composition to wrap an object, but serve different intent. The Proxy pattern controls access to the original object, adding functionality like lazy-loading, security, or remote access without altering the core behavior. The Decorator pattern, on the other hand, adds new behaviors or responsibilities to the wrapped object, extending its functionality dynamically at runtime. While both follow similar structural patterns, Proxy focuses on access control, and Decorator on incremental feature addition.

```csharp
// Proxy
public class LazyImage : IImage
{
    private RealImage _realImage;
    public void Display()
    {
        _realImage ??= new RealImage();
        _realImage.Display();
    }
}

// Decorator
public class LoggingImage : IImage
{
    private IImage _img;
    public LoggingImage(IImage img) => _img = img;
    public void Display()
    {
        Console.WriteLine("Logging...");
        _img.Display();
    }
}
```
---

## Q28: When should I use Active Record vs Repository Pattern?
The Active Record pattern is suitable for simple CRUD apps with straightforward domain logic, as it couples data access logic with the entity class itself. Repository Pattern is better for complex domains needing business logic separation, testability, and abstraction from data storage. Use Active Record for small, rapidly developed applications, and Repository for applications where maintainability, decoupling, and flexibility are important (e.g., enterprise applications or systems employing domain-driven design). Repository Pattern scales better for large applications with complex business logic.

```csharp
// Active Record
public class User
{
    public int Id { get; set; }
    public void Save() { /* save logic here */ }
}

// Repository
public interface IUserRepository
{
    User GetById(int id);
    void Save(User user);
}
```
---

## Q29: What are the drawbacks to the ActiveRecord pattern?
The ActiveRecord pattern tightly couples database operations to the entity, mixing business logic with data access logic. This reduces testability and violates the Single Responsibility Principle, as domain models become responsible for persistence. It can lead to difficulties when changing storage mechanisms or scaling the domain logic. Unit testing business logic may require a database connection, making tests slower and harder to maintain. With complex domains, maintaining correct boundaries becomes challenging, limiting code reuse and increasing risk of code smells.

```csharp
public class Product // Active Record
{
    public int Id { get; set; }
    public void Save() { /* Database logic here */ }
    public void CalculateDiscount() { /* Business logic mixed in */ }
}
```
---

## Q30: In OOP, what is the difference between the Repository Pattern and a Service Layer?
The Repository pattern encapsulates data access, serving as a collection-like interface for retrieving and storing aggregates. It abstracts the infrastructure concerns from business logic. The Service Layer pattern encapsulates business logic and application workflows, often orchestrating operations across multiple repositories. The repository focuses on persistence, while the service layer coordinates domain activities, policies, transactions, or external integrations. Keeping these responsibilities separate supports a clean architecture, easier testing, and improved code organization.

```csharp
public interface IOrderService
{
    void PlaceOrder(Order order);
}

public class OrderService : IOrderService
{
    private readonly IOrderRepository _repo;
    public OrderService(IOrderRepository repo) => _repo = repo;
    public void PlaceOrder(Order order)
    {
        // Business logic
        _repo.Add(order);
    }
}
```
---

## Q31: What are some advantages of using Dependency Injection?
Dependency Injection (DI) helps in decoupling a class from its dependencies, making code more modular, easier to test, and maintain. You can swap implementations (e.g., for unit testing) without changing the client code. DI promotes adherence to SOLID principles, especially Dependency Inversion. It also simplifies configuration, encourages loose coupling, and improves maintainability by centralizing object creation. In .NET, DI is widely supported via the built-in IoC container and frameworks like Autofac, Unity, etc.

```csharp
public class EmailService { }

public class Notification
{
    private readonly EmailService _emailService;
    public Notification(EmailService service) => _emailService = service;
}

// .NET built-in DI
services.AddTransient<EmailService>();
services.AddTransient<Notification>();
```
---

## Q32: What is the Command and Query Responsibility Segregation (CQRS) Pattern?
CQRS is an architectural pattern that separates read operations (queries) from write operations (commands) in an application. By decoupling the data models for reading and writing, CQRS improves scalability and supports optimization for different workloads (e.g., caching, denormalization for queries). It enables independent scaling of command and query sides and is often combined with event sourcing for audit trails. This pattern is suitable for complex domains with frequent changes, collaborative environments, or systems requiring high performance reads and writes.

```csharp
public class CreateOrderCommand { 
    public int ProductId; 
    public int Quantity; 
}
// Command Handler
public class CreateOrderHandler
{
    public void Handle(CreateOrderCommand cmd) { /* write logic */ }
}
// Query Handler
public class OrdersQuery
{
    public IEnumerable<Order> GetOrders() { /* query logic */ }
}
```
---

## Q33: Name some benefits of CQRS Pattern
CQRS allows independent scaling of reads and writes, supports distinct models optimized for queries and commands, and enables easier implementation of security or validation policies. By decoupling logic, it simplifies code and enables use of event sourcing, supporting audit trails and history. CQRS encourages code organization, making the distinction between command and query operations explicit. This results in better maintainability, flexibility for evolving requirements, and easier performance optimizations.

```csharp
public interface ICommandHandler<TCommand> { 
    void Handle(TCommand command); 
}
public interface IQueryHandler<TQuery, TResult> { 
    TResult Handle(TQuery query); 
}
```
---

## Q34: Describe what is the Event Sourcing Pattern
Event Sourcing persistently stores the state of a system as a series of events, rather than just the current state. Every state-changing operation is stored as an immutable event. The current state can always be rebuilt by replaying those events. Event Sourcing enables auditability, traceability, and temporal queries (“how did we get here?”). It's useful for domains requiring history tracking, audit trails, or synchronization between systems. Event sourcing is often combined with CQRS for resilience and consistency.

```csharp
public class Event { public string Name; public DateTime Time; }
public class EventStore
{
    private List<Event> _events = new();
    public void Save(Event e) => _events.Add(e);
    public IEnumerable<Event> GetEvents() => _events.AsEnumerable();
}
```
---

## Q35: Explain the use of Claim Check Pattern in Azure Event Grid
The Claim Check pattern is used in messaging systems to avoid sending large payloads by passing a small reference (the “claim check”) instead. In Azure Event Grid, large dataset payloads are stored in external storage (like Azure Blob Storage), while the event message contains a reference (URL or key) to it. Consumers retrieve the full data as needed. This approach reduces message size, improves performance, reliability, and lowers network usage by decoupling event metadata from large payloads.

```csharp
public class EventData
{
    public string BlobUrl { get; set; } // reference to actual data
    public string EventId { get; set; }
}
```
---

## Q36: What are the difference between a Static class and a Singleton class?
A static class cannot be instantiated or inherited and only contains static members, accessed via the class name. It is suitable for utility or helper methods. A singleton class is a design pattern ensuring only one instance of a class exists throughout the application’s lifetime, typically achieved with a private constructor and static property. Unlike static classes, singletons can implement interfaces and maintain state. Singleton allows lazy initialization and dependency injection, while static class is initialized before first usage.

```csharp
public static class MathHelper
{
    public static int Add(int a, int b) => a + b;
}

public class Singleton
{
    private static Singleton _instance;
    private Singleton() { }
    public static Singleton Instance => _instance ??= new Singleton();
}
```
---

## Q37: What is Adapter Pattern?
The Adapter pattern allows incompatible interfaces to work together by bridging differences between them. It wraps an existing class with a new interface, enabling clients to use it as if it implemented the required contracts. This pattern allows reuse of legacy or third-party code without modifying the source. It's useful when integrating systems or migrating to new interfaces, and is common in .NET, e.g., adapting data sources or APIs.

```csharp
// Old API
public class OldLogger { 
    public void LogMessage(string msg) => Console.WriteLine(msg); 
}
// New Interface
public interface ILogger { 
    void Log(string message); 
}
// Adapter
public class LoggerAdapter : ILogger
{
    private readonly OldLogger _oldLogger;
    public LoggerAdapter(OldLogger oldLogger) => _oldLogger = oldLogger;
    public void Log(string message) => _oldLogger.LogMessage(message);
}
```
---

## Q38: What does program to interfaces, not implementations mean?
Programming to interfaces entails coding against abstractions rather than concrete classes, enhancing flexibility and testability. It means depending on contracts (interfaces or abstract classes) that define expected behaviors, not the underlying implementation. This principle enables easy swapping of implementations (e.g., mocks for testing), encourages loose coupling, and promotes adherence to SOLID principles. It enables APIs to evolve, improves maintainability, and supports DI frameworks.

```csharp
public interface IPayment
{
    void Pay(decimal amount);
}

public class CreditCardPayment : IPayment { 
    public void Pay(decimal amount) { /* ... */ } 
}

public void ProcessPayment(
    IPayment payment) { payment.Pay(100); 
}
```
---

## Q39: What is Prototype pattern?
The Prototype pattern is a creational pattern where you create new objects by copying an existing object (the prototype), rather than instantiating new ones directly. This allows for object creation with complex initialization, or when direct instantiation is costly. In .NET, this is commonly implemented using the `ICloneable` interface. Prototype produces copies that can be shallow or deep, depending on requirements.

```csharp
public class Person : ICloneable
{
    public string Name { get; set; }
    public object Clone() => MemberwiseClone();
}
```
---

## Q40: What is Interpreter pattern?
The Interpreter pattern defines a representation for a grammar and an interpreter to process sentences in that grammar. It is used for parsing and evaluating expressions, commands, or scripts. In .NET, it is often used in the creation of scripting engines, expression evaluators, or domain-specific languages. Each rule in the grammar is represented by a class, and the pattern supports recursive composition for complex expressions.

```csharp
public interface IExpression
{
    int Interpret();
}
public class Number : IExpression
{
    private int _number;
    public Number(int number) => _number = number;
    public int Interpret() => _number;
}
public class Add : IExpression
{
    private IExpression _left, _right;
    public Add(IExpression left, IExpression right)
    { _left = left; _right = right; }
    public int Interpret() => _left.Interpret() + _right.Interpret();
}

// Usage
var expr = new Add(new Number(1), new Number(2));
Console.WriteLine(expr.Interpret()); // 3
```
---

## Q41: What is Command pattern?
The Command pattern encapsulates a request as an object, allowing users to parameterize clients with different requests and support features like undo, logging, or queuing. Rather than sending a method call directly, a command object encapsulates method parameters, the receiver, and the action. In .NET, Command pattern is commonly used in UI frameworks for button actions or task scheduling.

```csharp
public interface ICommand
{
    void Execute();
}
public class PrintCommand : ICommand
{
    public void Execute() => Console.WriteLine("Print!");
}
public class Invoker
{
    public void StoreAndExecute(ICommand cmd) => cmd.Execute();
}
```
---

## Q42: What is Facade pattern?
The Facade pattern provides a simplified interface to a subsystem, shielding clients from complex dependencies. It delegates client requests to appropriate subsystem objects. By encapsulating complexity, Facade helps decouple subsystems, improves usability, and organizes code logically. In .NET, facades are often used for providing simplified APIs to complex frameworks or libraries.

```csharp
public class MediaFacade
{
    private AudioPlayer _audio = new();
    private VideoPlayer _video = new();
    public void PlayMedia() { _audio.Play(); _video.Play(); }
}
```
---

## Q43: What is the Chain of Responsibility pattern?
The Chain of Responsibility pattern passes a request along a chain of handlers until one of the handlers processes it. Each handler contains a reference to the next. This pattern decouples the sender and receivers, allowing dynamic control flow and flexible addition of new handlers. In .NET, it’s useful for event processing, middleware, or logging systems.

```csharp
public abstract class Handler
{
    protected Handler _next;
    public void SetNext(Handler next) => _next = next;
    public abstract void Handle(string request);
}

public class ConcreteHandlerA : Handler
{
    public override void Handle(string request)
    {
        if (request == "A") Console.WriteLine("Handled by A");
        else _next?.Handle(request);
    }
}
```
---

## Q44: What is Abstract Factory pattern?
The Abstract Factory pattern defines an interface for creating families of related or dependent objects without specifying exact classes. It enables your code to work with various product families interchangeably. In .NET, this helps create platform-specific classes or variants of products as a cohesive unit, supporting Open/Closed Principle and code extensibility.

```csharp
public interface IUIFactory
{
    IButton CreateButton();
    ITextBox CreateTextBox();
}

public class WinUIFactory : IUIFactory
{
    public IButton CreateButton() => new WinButton();
    public ITextBox CreateTextBox() => new WinTextBox();
}
```
---

## Q45: When should I use Composite design pattern?
Use the Composite pattern when you need to treat individual objects and compositions of objects uniformly, such as representing tree structures (e.g., file system directories, UI hierarchies). Composite allows clients to operate on elements and groups of elements the same way. This pattern is ideal for building hierarchical structures where nodes can contain other nodes, supporting recursive composition.

```csharp
public abstract class Component
{
    public abstract void Display();
}

public class Leaf : Component
{
    public override void Display() => Console.WriteLine("Leaf");
}

public class Composite : Component
{
    private List<Component> _children = new();
    public void Add(Component c) => _children.Add(c);
    public override void Display()
    {
        Console.WriteLine("Composite");
        foreach (var child in _children) child.Display();
    }
}
```

## Q46: What is Observer pattern?

The Observer pattern is a behavioral design pattern where an object, called the subject, maintains a list of its dependents, called observers, and notifies them of any state changes. This enables a one-to-many relationship between objects, so when one changes, all its dependents are updated automatically. It is widely used in event-driven systems, such as user interfaces or messaging systems, where multiple components need to react to changes or events. The pattern decouples the subject from the observers, allowing flexible addition or removal of observers at runtime. In .NET, this pattern is often seen in the IObservable/IObserver interfaces or via event/delegate mechanisms. It encourages loose coupling, which enhances scalability and maintainability. However, care should be taken to manage observer subscriptions to avoid memory leaks.
```csharp
public interface IObserver { 
    void Update(); 
}
public class ConcreteObserver : IObserver { 
    public void Update() => Console.WriteLine("Notified!"); }
public class Subject {
    private List<IObserver> observers = new();
    public void Attach(IObserver o) => observers.Add(o);
    public void Notify() { 
        foreach (var o in observers) 
            o.Update(); 
    }
}
```
---

## Q47: What is Bridge pattern?

The Bridge pattern is a structural design pattern that decouples an abstraction from its implementation, allowing the two to vary independently. Rather than tightly coupling an abstraction to its implementation, the Bridge pattern introduces an interface (the bridge) that both the abstraction and implementation inherit. This enables changing either the abstraction or the implementation across class hierarchies without affecting the other. It is especially useful when both the abstraction and implementation may have multiple variations and need to be extended in future. Common use cases include GUI toolkits or persistence frameworks where you want to change the platform or implementation without altering the core logic. This pattern provides better flexibility and reduces code duplication, making the codebase easier to manage and scale.
```csharp
public interface IRenderer { 
    void Render(string shape); 
}
public class VectorRenderer : IRenderer { 
    public void Render(string shape) => Console.WriteLine($"Vector: {shape}"); 
}
public class Shape {
    protected IRenderer renderer;
    public Shape(IRenderer r) { renderer = r; }
    public virtual void Draw() => renderer.Render("Shape");
}
public class Circle : Shape {
    public Circle(IRenderer r) : base(r) { }
    public override void Draw() => renderer.Render("Circle");
}
```
---

# Senior

## Q48: Explain usage of Service Locator Pattern

The Service Locator pattern provides a central registry or locator object that clients use to obtain services and dependencies at runtime. Rather than directly instantiating dependencies or using constructor injection, clients request the required service from the Service Locator. This pattern is useful in scenarios where dependency injection is not feasible, such as legacy systems or when dynamic service resolution is needed. However, overuse can lead to hidden dependencies and a codebase that’s harder to reason about or test, since dependencies are resolved at runtime. It's often considered an anti-pattern in modern code due to these drawbacks. Still, it can be useful for decoupling service creation from usage, especially in plugin architectures or frameworks.
```csharp
public class ServiceLocator {
    private static Dictionary<Type, object> services = new();
    public static void Register<T>(T service) => services[typeof(T)] = service;
    public static T Get<T>() => (T)services[typeof(T)];
}
```
---

## Q49: What are some disadvantages of Dependency Injection?

While Dependency Injection (DI) improves flexibility and testability, it also introduces some challenges. One downside is increased complexity, as tracing dependencies can become difficult, especially in large projects. DI frameworks may reduce readability by abstracting away object creation. Debugging can be harder, as objects are instantiated by the container rather than explicitly. Incorrect configuration or circular dependencies can result in run-time errors that are hard to diagnose. DI may also lead to over-engineering, with interfaces and abstractions added just for DI’s sake. Performance overhead from the DI container’s initialization or reflection-based service resolution may occur, though it is rarely significant.
```csharp
public interface IService { 
    void Serve(); 
}
public class Service : IService { 
    public void Serve() => Console.WriteLine("Served"); 
}
public class Client {
    private IService service;
    public Client(IService svc) { service = svc; }
    public void Start() => service.Serve();
}
```
---

## Q50: What is the difference between Strategy design pattern and State design pattern?

Both Strategy and State patterns encapsulate algorithms or behaviors in separate classes, but they differ in intent and usage. The Strategy pattern allows selecting an algorithm or behavior at runtime; it enables the client to pick which strategy to use. The State pattern, on the other hand, allows an object to alter its behavior when its internal state changes—transitions are usually managed internally by the context object, not externally. Strategies are interchangeable and independent of context state, while states represent different conditions or phases of an object. Clients choose strategies explicitly, whereas states often transition automatically within the object. Thus, Strategy is for interchangeable algorithms, State is for objects with dynamic behavior tied to their state.
```csharp
// Strategy
public interface IStrategy { 
    void Execute(); 
}
public class ConcreteStrategyA : IStrategy { 
    public void Execute() => Console.WriteLine("A"); 
}
// State
public interface IState { 
    void Handle(); 
}
public class ConcreteStateA : IState { 
    public void Handle() => Console.WriteLine("State A"); 
}
```
---

## Q51: What is relationship between Repository and Unit of Work?

The Repository pattern provides an abstraction over data access, focusing on collections of domain objects, while the Unit of Work (UoW) pattern maintains a list of changes for a business transaction and coordinates their atomic persistence. Typically, repositories work within a Unit of Work context: repositories retrieve and manipulate objects, and the Unit of Work tracks changes to those objects and commits them as a single transaction. The Repository abstracts queries and the Unit of Work ensures changes across multiple repositories are consistent and transactional. This promotes separation of concerns, improved testability, and minimizes redundant database operations.
```csharp
public interface IRepository<T> { 
    void Add(T item); 
}
public interface IUnitOfWork { 
    void Commit(); 
}
```
---

## Q52: What is Flyweight pattern?

The Flyweight pattern is a structural design pattern that minimizes memory use by sharing as much data as possible between similar objects. It is useful when an application needs to create a large number of objects that share most of their state—this shared state is called intrinsic state, while unique state is extrinsic and stored externally to the flyweight. A common example is rendering characters in a text editor, where most character formatting can be shared. This pattern improves memory efficiency and performance, but can increase complexity of managing state.
```csharp
public class Flyweight {
    private string sharedState;
    public Flyweight(string state) { sharedState = state; }
    public void Operation(string uniqueState) =>
        Console.WriteLine($"Shared: {sharedState}, Unique: {uniqueState}");
}
```
---

## Q53: Explain what is Composition over Inheritance?

Composition over Inheritance is a principle that suggests building complex objects by combining simpler, reusable components (composition) rather than using inheritance hierarchies. Favoring composition allows greater flexibility, as behavior can be changed or extended by swapping components without modifying or extending classes. This reduces coupling, avoids the fragility of deep inheritance, and promotes code reuse. In C#, this is often achieved via interfaces and aggregation—instead of subclassing, you use fields or properties referring to other objects with desired behavior. This approach supports runtime behavior changes and adheres to the SOLID principles, especially Open/Closed and Single Responsibility.
```csharp
public interface IEngine { 
    void Start(); 
}
public class Car { 
    private IEngine engine; 
    public Car(IEngine e) { engine = e; } 
    public void Start() => engine.Start(); 
}
```
---

## Q54: Why shouldn't I use the Repository Pattern with Entity Framework?

Entity Framework already acts as a repository and unit of work, providing methods for querying, adding, and saving entities. Implementing a custom repository around EF often results in redundant code or abstraction that adds little value and limits EF’s advanced capabilities like change tracking and LINQ queries. Over-abstracting can make code harder to maintain and test, and sometimes hides useful EF features. It’s often better to use EF directly for data access, reserving the Repository pattern for cases where you need a different abstraction (e.g., non-EF data sources or complex aggregates).
```csharp
// Using DbSet<Employee> as a repository:
public class MyDbContext : DbContext { 
    public DbSet<Employee> Employees { get; set; } 
}
```
---

## Q55: How is Bridge pattern different from Adapter pattern?

The Bridge pattern is used to separate abstraction from implementation to let both evolve independently, and is applied at design time to extend functionality. The Adapter pattern, however, converts the interface of an existing object to make it compatible with another interface, allowing classes with incompatible interfaces to work together. Bridge is about flexibility and extensibility, typically used when both interfaces might change. Adapter is about compatibility and is often used when integrating existing code with new code. Bridge involves two hierarchies (abstraction and implementation); Adapter wraps an object to provide a different interface.
```csharp
// Adapter
public class OldService { 
    public void OldMethod() { } 
}
public interface INewService { 
    void NewMethod(); 
}
public class Adapter : INewService { 
    private OldService _old; 
    public Adapter(OldService o) { _old = o; } 
    public void NewMethod() => _old.OldMethod(); 
}
```
---

## Q56: How should I be grouping my Repositories when using Repository Pattern?

Repositories should be grouped by aggregate roots, not by entity. Each repository should encapsulate all data access logic for the aggregate root and its subordinate objects, preventing direct access to child entities. Avoid creating a repository for each table—focus on domain consistency and business logic grouping. For example, use an OrderRepository for the Order aggregate; don’t create separate repositories for OrderLine or Product unless they are independent aggregate roots. This approach maintains domain integrity and enforces business rules, aligning with Domain-Driven Design principles regarding aggregates.
```csharp
public class OrderRepository : IRepository<Order> { /* methods for order and lines */ }
```
---

## Q57: Is Repository Pattern as same as Active Record Pattern?

No, the Repository pattern abstracts data access and enables working with data as collections, separate from business logic. The Active Record pattern couples the object with the data access logic, typically meaning the object contains methods to save, load, or delete itself. Repository keeps business entities POCOs (plain objects) and encourages separation of concerns, while Active Record makes each entity responsible for its own persistence. Repository enables unit testing and complex business rules, Active Record is simpler but less flexible in complex domains.
```csharp
// Active Record
public class Employee { 
    public void Save() { /*...*/ } 
}
// Repository
public class EmployeeRepository { 
    public void Save(Employee e) { /*...*/ } 
}
```
---

## Q58: What will you choose: Repository Pattern or "smart" business objects?

Repository Pattern is preferable when you have complex business logic, need separation of data and behavior, or when unit testing is important. It allows for easier maintenance and swapping of data stores, and complies with clean architecture and DDD. “Smart” business objects (Active Record) are preferable for simple CRUD systems or demos, where rapid development matters more than scalability. Generally, Repository provides greater flexibility, testability, and maintainability for non-trivial applications.
```csharp
// Repository Example
public class ProductRepository { 
    public Product GetById(int id) { /*...*/ } 
}
```
---

## Q59: Could you explain some benefits of Repository Pattern?

The Repository pattern abstracts the data access layer, enabling the underlying storage to be changed without affecting business logic. This separation of concerns improves testability by allowing data access to be mocked or swapped. It provides a consistent interface for querying and persisting objects, reduces duplication, and enforces domain rules at the aggregate root level. The pattern simplifies unit testing and supports clean, maintainable code. It also centralizes queries and transactions, making maintenance and refactoring easier.
```csharp
public interface IRepository<T> { 
    IQueryable<T> GetAll(); 
    void Add(T entity); 
}
```
---

## Q60: Why would I ever use a Chain of Responsibility over a Decorator?

Use Chain of Responsibility when you need to process a request through a sequence of handlers, where each handler can either handle or pass the request along the chain. It’s useful for workflows, pipelines, or when each handler may or may not process the input. Decorator is used for dynamically adding behavior to objects, not for passing or handling requests in turn. Chain of Responsibility is about delegation and flexible responsibility, while Decorator is about composition and extending object functionality.
```csharp
public abstract class Handler { 
    protected Handler next; 
    public void SetNext(Handler n) => next = n; 
    public abstract void Handle(string req); 
}
```
---

## Q61: When would you use the Builder Pattern? Why not just use a Factory Pattern?

Use Builder Pattern when object creation requires several steps or complex construction logic, or when you need to construct different representations of the same object. Builder separates construction from representation, often supporting chained method calls for readability. Factory Pattern is better for simple scenarios where object construction is straightforward and doesn’t require intermediate steps or complex setup. Builder is useful for complex objects (e.g., creating complex aggregates or hierarchies), while Factory is for polymorphic object creation.
```csharp
public class CarBuilder { 
    private Car car = new Car(); 
    public CarBuilder SetColor(string c) { 
        car.Color = c; 
        return this; 
    } 
    public Car Build() => car; 
}
```
---

# Expert

## Q62: What's the difference between the Dependency Injection and Service Locator patterns?

Dependency Injection (DI) provides dependencies directly through constructors, properties, or methods, making dependencies explicit and traceable. The Service Locator pattern, on the other hand, keeps dependencies hidden; clients request them from a central registry at runtime. DI promotes clearer code, better testability, and more maintainable dependencies. Service Locator can lead to hidden dependencies and is harder to test, though it offers dynamic resolution. DI encourages the code to declare dependencies up front, while Service Locator hides them, potentially increasing code complexity.
```csharp
// DI
public class Client { 
    public Client(IService s) { } 
}
// Service Locator
public class Client { 
    public void Use() { 
        var s = ServiceLocator.Get<IService>(); 
    } 
}
```
---

## Q63: What is the difference between the Template patterns and the Strategy pattern?

The Template Method pattern defines the skeleton of an algorithm in a base class, allowing subclasses to override certain steps without changing the algorithm structure. It uses inheritance. The Strategy pattern defines a family of algorithms, encapsulated as objects, and makes them interchangeable at runtime. It uses composition. Template fixes the sequence, delegates steps; Strategy allows replacing entire algorithms. Template is for invariant algorithms; Strategy for variations.
```csharp
// Template Method
abstract class AbstractClass { 
    public void Template() { 
        Step1(); 
        Step2(); 
    } 
    protected abstract void Step1(); 
    protected virtual void Step2() { } 
}
// Strategy
public interface IAlgorithm { 
    void Execute(); 
}
```
---

## Q64: Explain difference between the Facade, Proxy, Adapter and Decorator design patterns?

Facade provides a simplified interface to a complex subsystem. Proxy controls access to an object, often adding security, logging, or lazy loading. Adapter makes incompatible objects work together by converting one interface to another. Decorator adds additional responsibilities or behavior to an object dynamically. Facade is about simplification, Proxy about controlling access, Adapter about compatibility, and Decorator about extended functionality.
```csharp
// Facade
public class Facade { 
    private Subsystem s = new(); 
    public void Operation() => s.DoWork(); 
}
```
---

## Q65: Could you explain the difference between Façade vs. Mediator?

Facade hides complexity by providing a unified interface to a subsystem. It doesn’t manage dependencies or communication between subsystem classes. Mediator, in contrast, centralizes communication among objects, facilitating decoupled interaction between colleagues. With Facade, subsystem components still interact directly; with Mediator, all communications go through the mediator. Use Facade for simplifying external usage; Mediator for complex communication patterns.
```csharp
// Mediator Example
public interface IMediator { 
    void Notify(object sender, string evt); 
}
```
---

## Q66: Can we use the CQRS without the Event Sourcing?

Yes, CQRS (Command Query Responsibility Segregation) and Event Sourcing are separate patterns that can be used independently. CQRS focuses on separating the read and write models for scalability and flexibility, while Event Sourcing stores state as a sequence of events. You can implement CQRS with traditional CRUD or relational storage without capturing events as the source of truth. Each pattern can be adopted separately or together based on application needs.
```csharp
// CQRS (no event sourcing)
public interface ICommand { }
public interface IQuery<T> { }
```
---

## Q67: Could you explain what is the Deadly Diamond of Death?

The "Deadly Diamond of Death" is a term from multiple inheritance in object-oriented programming, referring to the ambiguity that arises when a class inherits from two classes that have a common ancestor. The inheritance diagram forms a diamond shape, and if both parent classes override a method from the common ancestor, it’s unclear which version the child calls. C# avoids this by not supporting multiple inheritance with classes (only interfaces). With interfaces, explicit implementation resolves ambiguity.
```csharp
interface IA { void Foo(); }
interface IB : IA { }
interface IC : IA { }
class D : IB, IC { void IA.Foo() { } }
```
---