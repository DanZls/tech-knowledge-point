# Entry

## Q1: What is Entity Framework?

Entity Framework (EF) is an open-source Object-Relational Mapper (ORM) for .NET applications. It provides an abstraction layer that allows developers to interact with a database using .NET objects, eliminating the need for most of the data-access code that developers usually have to write. EF supports LINQ queries, change tracking, updates, schema migrations, and more. It can work with different database engines such as SQL Server, SQLite, PostgreSQL, and others.

```csharp
public class MyDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
```

---

## Q2: What are the benefits of using EF?

Entity Framework provides several benefits, including reduced coding for data access, support for LINQ queries for complex data manipulation, and database abstraction. It provides a strong type-safe API and has the capability to manage data relationships efficiently. Additionally, it supports three primary approaches: Database First, Model First, and Code First, allowing flexibility in development style. EF also supports automatic migration and is integrated with the ASP.NET framework.

```csharp
var products = myDbContext.Products.Where(p => p.Price > 100).ToList();
```

---

## Q3: Mention in what all scenarios Entity Framework can be applicable?

Entity Framework can be applicable in scenarios where there's a need for rapid development with minimal database interaction code. It's suitable for applications requiring object-relational mapping without a deep understanding of SQL. EF can be used in web applications, desktop applications, and services where .NET is used extensively. It is also used when there's a requirement for strongly-typed data models and LINQ querying.

```csharp
using (var context = new MyDbContext())
{
    var products = context.Products.ToList();
}
```

---

# Junior

## Q4: What is pluralize and singularize in the Entity Framework?

Pluralize and singularize are features in Entity Framework that automatically convert table names to their singular or plural form when generating code. This is particularly used in the Code First and Model First approaches to create an intuitive connection between class names (singular) and table names (plural) in the database. For example, a class named `Product` might automatically map to a `Products` table.

---

## Q5: Mention what is Code First Approach and Model First Approach in Entity Framework?

The Code First Approach allows developers to define their model using C# or VB.NET classes and then generate a database based on those classes. This approach makes it easier to work with domain-driven design and unit tests. The Model First Approach, on the other hand, involves creating a model in the Entity Framework Designer and generating the database from that model. It's suitable when starting from a visual model and you want to generate the database schema.

```csharp
// Code First Example
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

---

## Q6: What is Code First approach in Entity Framework?

The Code First approach enables developers to define their data models using C# or VB.NET classes. Entity Framework then uses these classes to automatically create the database. This approach is beneficial for those focusing on domain-driven design and allows for easy integration with existing unit tests. The approach also supports database versioning and migrations, enabling smooth schema evolution.

```csharp
public class MyDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
```

---

## Q7: What is the purpose of a DBContext class?

The `DbContext` class is the primary class for interacting with the database in EF. It acts as a bridge between the domain or entity classes and the database, managing the object-relational mapping and data operations. It provides methods to query and save data, manage change tracking, handle concurrency, and configure relationships. `DbContext` is essential for managing the lifecycle of entities and executing queries.

```csharp
public class MyDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
```

---

## Q8: What is Conceptual Model?

The Conceptual Model in Entity Framework is part of the Entity Data Model (EDM) that defines the application-centric view of the data. It describes the entities, their relationships, and their attributes without considering how they are mapped to the database. This model reflects how the data is perceived in the .NET application and is specified in an XML format within an EDMX file for Model First or Database First approaches.

---

## Q9: What is migration in Entity Framework?

Migration in Entity Framework refers to the process of evolving the database schema over time through incremental changes. It helps in keeping the database in sync with the application model. EF Migrations allow developers to apply changes like adding or removing tables, columns, and relationships without losing existing data. It also provides commands for applying these migrations to a database.

```csharp
Add-Migration InitialCreate
Update-Database
```

---

## Q10: What is Mapping?

Mapping in Entity Framework refers to the process of linking entities in the conceptual model to tables in the database schema. It involves defining how properties in entity classes map to columns in a database and how relationships between entities map to foreign keys. Mapping ensures that operations on the conceptual model are accurately reflected in the database operations.

---

## Q11: What is Storage Model?

The Storage Model in Entity Framework is the part of the Entity Data Model (EDM) that describes the database schema, including tables, columns, and relationships. It represents how the data is physically stored in the database. This model is used together with the Conceptual Model and Mapping to define how entities in an application interact with the underlying database schema.

---

## Q12: What are scalar and navigation properties in Entity Framework?

Scalar properties in Entity Framework refer to simple attributes or fields of an entity that map to individual columns of a table, such as `int`, `string`, or `DateTime`. Navigation properties, on the other hand, represent relationships between entities, such as one-to-many or many-to-many. They allow access to related entities and are automatically managed by EF to handle data consistency and integrity.

```csharp
public class Product
{
    public int Id { get; set; } // Scalar property
    public string Name { get; set; } // Scalar property
    public Category Category { get; set; } // Navigation property
}
```

---

## Q13: What are complex types in Entity Framework?

Complex types in Entity Framework are non-scalar properties within an entity that group multiple related properties together but do not have a key or identity property. They map to columns in a single table and cannot exist independently of the entity they're part of. Complex types are useful for encapsulating details like an address or contact information within an entity.

```csharp
public class Address
{
    public string Street { get; set; }
    public string City { get; set; }
}

public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; }
    public Address Address { get; set; } // Complex Type
}
```

---

# Mid

## Q14: Could you explain the difference between Optimistic vs Pessimistic locking?

Optimistic locking assumes conflicts are rare and checks for conflicts only when changes are saved, typically by using versioning or timestamps. It's suitable for scenarios with low contention. Pessimistic locking prevents other transactions from modifying data by acquiring locks on data when a read or write occurs, common in high-contention environments to ensure data integrity. Pessimistic locking can lead to reduced concurrency and potential deadlocks.

---

## Q15: What is the importance of EDMX file in Entity Framework?

The EDMX file in Entity Framework is an XML file used in Database First and Model First approaches. It contains the Entity Data Model (EDM), describing the conceptual, storage, and mapping details. It serves as the bridge between the database and application code, enabling generation of EF classes and ensuring consistency between the model and the underlying database schema.

---

## Q16: What are POCO classes in Entity Framework?

POCO (Plain Old CLR Object) classes in Entity Framework are simple .NET classes that have no dependency on EF-specific constructs or libraries. They represent data entities and are used in Code First and sometimes Model First approaches to define the structure of the data model. POCO classes enhance testability and maintain a clear separation between the data model and the database logic.

```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

---

## Q17: What are the different approaches supported in the Entity Framework to create Entity Model?

Entity Framework supports three main approaches to creating an entity model: Database First, Model First, and Code First. Database First involves reverse engineering an existing database to generate a model. Model First allows designing a model diagrammatically, which then generates the database. Code First lets developers write classes to define the model, which EF uses to generate the database schema.

---

## Q18: Can you explain Lazy Loading in a detailed manner?

Lazy Loading in Entity Framework is a feature where related data is automatically loaded from the database when accessed for the first time. It defers the retrieval of related data until it is specifically requested. Lazy loading is achieved by using virtual navigation properties. This can improve performance by loading only the necessary data but can result in multiple queries if not managed properly.

```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public virtual Category Category { get; set; } // Lazy Loading
}
```

---

## Q19: What is EF Data Access Architecture?

EF Data Access Architecture involves several components: the `DbContext`, which manages database connections and transactions; the entity classes that represent the data model; and LINQ queries for data access. The architecture also involves handling concurrency, connection resiliency, and managing migrations. It provides a comprehensive framework for applications to interact with the database using a high-level, object-oriented API.

---

## Q20: What are the advantages and disadvantages of Database First Approach?

Advantages of the Database First Approach include support for existing databases, graphical visualization of models, and ease of integration with legacy systems. It automates model generation from the database schema, saving time in setting up the model. However, it can complicate managing complex mappings, lacks flexibility compared to Code First, and changes to the database require manual synchronization with the model.

```csharp
// Generated classes represent tables in the database
public partial class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

---

## Q21: What are the components of Entity Framework Architecture?

Entity Framework architecture consists of several key components: the Entity Data Model (EDM), Object Services, LINQ to Entities, Entity SQL, the Entity Client Data Provider, and the Connection and Metadata Services. The EDM is a model that represents the data described in terms of entities and relationships. Object Services handle object tracking and materialization. LINQ to Entities provides a LINQ-based querying method for Entity Framework. Entity SQL is a SQL-like language for querying against the EDM. The Entity Client Data Provider acts as the bridge between Entity Framework and the underlying data source. Connection and Metadata Services manage the connection to the database and handle metadata operations. These components work together to provide a comprehensive data access layer that abstracts complex database operations into more manageable entities and relationships.

```csharp
public class Product
{
    public int ProductId { get; set; }
    public string Name { get; set; }
}

using (var context = new MyDbContext())
{
    var products = context.Products.ToList();
}
```
---

## Q22: What are the advantages of Model First Approach?

The Model First approach in Entity Framework allows developers to design their database using visual modeling tools, which then generate the database schema. The advantages include ease of use for those who prefer visual design over coding. It helps in rapidly designing databases and visualizing complex relationships. It's useful in scenarios where the database hasn't been created yet, allowing a more guided development process. Model First also supports iterative development, making it easier to adjust the model and regenerate the schema as the application evolves. Additionally, it generates consistent and maintainable code and database structures, aligning with a central model. 

```csharp
// Model designed in a visual tool, then code generated:
public class Customer
{
    public int CustomerId { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```
---

## Q23: Explain how you can load related entities in EF?

Entity Framework provides multiple ways to load related entities: Eager Loading, Lazy Loading, and Explicit Loading. Eager Loading retrieves related entities as part of the initial query using the `Include` method, which can reduce round trips to the database. Lazy Loading delays the loading of related data until it is specifically accessed in the code, which is achieved by marking navigation properties as virtual. Explicit Loading is manually loading related data only when needed, using methods such as `Load` on the navigation property. Each method has its use-case depending on performance considerations and the specific data access strategy required.

```csharp
// Eager Loading
var blogs = context.Blogs.Include(b => b.Posts).ToList();

// Explicit Loading
var blog = context.Blogs.Find(1);
context.Entry(blog).Collection(b => b.Posts).Load();
```
---

## Q24: What is Eager Loading?

Eager Loading is a strategy used by Entity Framework to load related entities as part of the query that retrieves the main entity or entities. This is accomplished using the `Include` method, allowing for related data to be loaded in a single query rather than multiple separate ones. Eager Loading is beneficial when an application requires related data immediately after loading the main entity, thus reducing potential additional database calls. However, it can lead to fetching more data than necessary, which might impact performance if not managed correctly. The `Include` method supports navigation properties to specify which related data should be included during the query execution.

```csharp
// Eager Loading with Include
var order = context.Orders.Include(o => o.OrderDetails).FirstOrDefault(o => o.Id == orderId);
```
---

## Q25: What is the role of Entity Client Data Provider?

The Entity Client Data Provider is a key component in the Entity Framework architecture that acts as a bridge between the Entity Data Model (EDM) and the actual database. Its primary role is to convert Entity SQL queries into SQL commands that can be executed against the database. This abstraction allows developers to work with a conceptual model without needing direct reference to the underlying database schema. It manages the communication between the application's domain model and the data source, ensuring that data operations remain consistent with the structure of the EDM.

```csharp
using (var context = new MyDbContext())
{
    var query = context.Products.SqlQuery("SELECT * FROM Products WHERE CategoryId = @p0", categoryId);
}
```
---

## Q26: How can we handle concurrency in Entity Framework?

Entity Framework provides a built-in mechanism to handle concurrency using optimistic concurrency control. This usually involves marking a column, such as a timestamp, with the `[ConcurrencyCheck]` attribute or by using a `RowVersion`. When multiple users try to update the same data, a concurrency exception is thrown if the data has changed since it was loaded. This allows you to inform users of the conflict and resolve the issue appropriately, such as refreshing the data or prompting users to retry their changes. Managing concurrency effectively ensures data integrity in multi-user environments.

```csharp
public class Product
{
    public int ProductId { get; set; }
    public string Name { get; set; }
    [ConcurrencyCheck]
    public int Stock { get; set; }
}

try
{
    context.SaveChanges();
}
catch (DbUpdateConcurrencyException ex)
{
    // Handle concurrency conflict
}
```
---

## Q27: Explain Lazy Loading, Eager Loading, and Explicit Loading?

Lazy Loading is the default behavior in Entity Framework where a related entity is automatically loaded the first time it is accessed. This is done by making navigation properties virtual. Eager Loading, on the other hand, retrieves related entities as part of the initial database query using the `Include` method, which can improve performance by reducing database round trips. Explicit Loading is manually loading related entities when necessary by calling methods such as `Load` on the navigation properties. Each approach has its own use-case scenarios depending on the performance and data access requirements.

```csharp
// Lazy Loading
public virtual ICollection<Post> Posts { get; set; }

// Eager Loading
var blogs = context.Blogs.Include(b => b.Posts).ToList();

// Explicit Loading
var blog = context.Blogs.Find(1);
context.Entry(blog).Collection(b => b.Posts).Load();
```
---

## Q28: What are the advantages/disadvantages of Code First Approach?

The Code First approach allows developers to define the domain model using C# classes, which Entity Framework then uses to generate the database schema. Advantages include a higher degree of flexibility as developers can work directly with C# classes. It simplifies deployment and version control since the database schema changes are managed through migrations. However, the Code First approach can be challenging when working with an existing database as it's mainly designed for new projects. Additionally, initial setup may require more manual configuration compared to Model First or Database First approaches.

```csharp
public class Blog
{
    public int BlogId { get; set; }
    public string Name { get; set; }
}
```
---

## Q29: What is Optimistic Locking?

Optimistic Locking is a concurrency control method used in Entity Framework that assumes multiple transactions can complete without affecting each other. Instead of a database lock, it uses versioning to detect conflicts. A version column or timestamp is typically used to track changes in a row. When an update occurs, Entity Framework checks whether the version of the row in the database matches the version that was fetched when the entity was loaded. If not, a concurrency exception is thrown. It minimizes locking and is efficient in scenarios with less likelihood of conflicts.

```csharp
public class Product
{
    public int ProductId { get; set; }
    public string Name { get; set; }
    [Timestamp]
    public byte[] RowVersion { get; set; }
}
```
---

## Q30: What’s the difference between LINQ to SQL and Entity Framework?

LINQ to SQL and Entity Framework are both ORM technologies from Microsoft, but they differ in scope and functionality. LINQ to SQL is directly tied to SQL Server and focuses on a one-to-one mapping to the database schema, suitable for simpler applications. Entity Framework, on the other hand, supports various database engines and is designed as a full-featured ORM with more complex mapping capabilities, such as inheritance and relationships. Entity Framework is more flexible and comprehensive in enterprise scenarios, while LINQ to SQL is easier to use for smaller, simpler applications.

```csharp
// LINQ to SQL example
var results = from p in dbContext.Products where p.Price > 100 select p;

// Entity Framework example
var results = context.Products.Where(p => p.Price > 100).ToList();
```
---

# Senior

## Q31: What are the disadvantages of using static DbContext?
Static DbContext can lead to several issues, primarily related to concurrency. Since DbContext is not thread-safe, using a static instance can cause data corruption and unexpected behavior when accessed concurrently by multiple threads. It also impedes the ability to handle Unit of Work patterns effectively, as transactions could overlap, leading to inconsistent states. Having a static DbContext means changes persist across multiple requests, which can be problematic in web applications where each request should generally operate independently. Performance issues could arise since the DbContext will hold more data in memory. Additionally, testing becomes difficult as unit tests might affect each other due to shared state. It also violates the Dependency Inversion Principle, making the system tightly coupled to the DbContext.

```csharp
public static class DbContextHolder
{
    public static MyDbContext Context { get; } = new MyDbContext();
}
```
---

## Q32: Which type of loading is good in which scenario?
Eager loading is suitable when you know you will need related data; it reduces the number of queries by loading related entities upfront. This is particularly useful when the relationships are not too large and are frequently accessed together, as it minimizes the overhead of multiple database round trips. Lazy loading is beneficial when related data isn't always necessary and can be loaded on demand, which can improve initial load times in these scenarios. However, it involves additional queries, potentially degrading performance in some cases. Explicit loading provides control to load related data manually, useful in situations where you need specific related data based on a condition. It strikes a balance where neither all nor none of the related entities need loading upfront.

```csharp
// Eager Loading
var order = context.Orders.Include(o => o.Items).FirstOrDefault(o => o.Id == 1);

// Lazy Loading (requires virtual navigation property and configuration)
var order = context.Orders.FirstOrDefault(o => o.Id == 1);
var items = order?.Items; // triggers database query

// Explicit Loading
var order = context.Orders.FirstOrDefault(o => o.Id == 1);
context.Entry(order).Collection(o => o.Items).Load();
```
---

## Q33: When would you use EF6 vs EF Core?
EF6 is ideal when working on existing applications that rely on mature, stable libraries or need features not yet fully supported in EF Core, such as certain advanced mapping scenarios or lazy loading without additional setup. It's also preferable for developers who require complete compatibility with older framework versions and tooling. EF Core, on the other hand, is beneficial for new projects or those targeting .NET Core due to its modular and cross-platform capabilities. It provides better performance and flexibility, supporting modern features like compiled queries and shadow properties. Although EF Core lacks some features of EF6, its ongoing development promises future enhancements and new features.

```csharp
// EF6
using (var context = new MyDbContext())
{
    var data = context.MyEntities.ToList();
}

// EF Core
using (var context = new MyDbContext())
{
    var data = context.MyEntities.ToList();
}
```
---

## Q34: Name some differences between Express vs Recoverable messages
Express messages in Microsoft messaging systems are volatile; they are stored only in memory and deliver faster but can be lost if the system crashes. On the other hand, recoverable messages are persistent, stored on disk to ensure delivery even in case of a system failure. Therefore, they provide reliability at the expense of performance. Recoverable messages are best for critical data that must not be lost while express messages suit non-critical, high-throughput situations where speed is a priority over reliability. This distinction allows developers to choose trade-offs between speed and reliability based on specific application needs.

```plaintext
// No code example is typically associated with these concepts as they are configuration settings in messaging services.
```
---

## Q35: Is DbContext thread safe?
DbContext is not thread-safe. It is designed to be used with a single thread, usually within the scope of a single HTTP request or unit of work in a console application. Using DbContext concurrently across multiple threads can lead to data corruption or inconsistent behavior since internal state management like change tracking and lazy loading is not designed for concurrency. To avoid problems, multiple instances of DbContext should be created and disposed of for different threads. Dependency Injection (DI) frameworks typically handle DbContext lifetimes efficiently by providing a new instance per request (or scope).

```csharp
// Usage scope per request or operation
using (var context = new MyDbContext())
{
    // Perform operations
}
```
---

## Q36: Why shouldn't I use the Repository Pattern with Entity Framework?
Using the Repository Pattern with Entity Framework is often considered redundant because EF itself implements a repository and unit of work pattern, rendering additional abstraction unnecessary. EF's built-in capabilities such as querying through LINQ, change tracking, and transactional behavior make custom repositories less beneficial and introduce complexity without significant gain. Custom repositories may hide EF's powerful querying capabilities and lead to more boilerplate code, reducing development productivity. However, in projects with multiple data sources or for abstracting away EF-specific code to simplify testing, repositories could still be useful albeit being less common.

```csharp
// Simplified direct use of EF
var users = context.Users.Where(u => u.IsActive).ToList();
```
---

## Q37: What are T4 templates?
T4 (Text Template Transformation Toolkit) templates are code generation tools integrated within Visual Studio that allow developers to generate code, text files, XML, or HTML. In the context of Entity Framework, T4 templates are used to generate entity classes and DbContext from the EDMX model. They support customization, enabling developers to tailor generated code to meet specific requirements. T4 templates use a combination of C# or Visual Basic .NET code and inline template syntax. This flexibility makes T4 templates powerful for automating repetitive tasks and maintaining consistency in generated code.

```plaintext
// Simple T4 template to generate a class
<#@ template language="C#" #>
<#@ output extension=".cs" #>
public class GeneratedClass
{
    public string Name { get; set; }
}
```
---

## Q38: What is relationship between Repository and Unit of Work?
The Repository pattern manages CRUD operations for a specific entity type, often implemented with an interface to abstract data access logic. In contrast, the Unit of Work pattern coordinates these repositories by managing transactions, ensuring a series of operations are completed as a single atomic unit. This pattern reduces multiple database calls and improves transaction management. The Unit of Work typically maintains a list of pending changes and commits them together, making it easier to handle complex operations involving multiple repositories. The two patterns together provide a higher-level abstraction, allowing developers to handle data access with more flexibility and consistency.

```csharp
public class UnitOfWork : IUnitOfWork
{
    private readonly MyDbContext _context;
    private IRepository<User> _userRepo;

    public IRepository<User> UserRepository 
        => _userRepo ??= new Repository<User>(_context);

    public void Save() => _context.SaveChanges();
}
```
---

## Q39: Could you explain Pessimistic locking?
Pessimistic locking is a concurrency control method where a record or resource is locked from access by others until a transaction is complete. It's used to prevent conflicts and ensure data integrity in environments with high contention. Under pessimistic locking, when a transaction modifies a record, other transactions are blocked from accessing it until the lock is released, thus preventing concurrent modifications that could cause conflicts. Although it ensures consistency, it can lead to reduced performance and potential deadlocks. It is typically used in systems where the data integrity is critical and contention for resources is high.

```csharp
// Pseudocode: Normally handled at the database level
BEGIN TRANSACTION;
SELECT * FROM MyTable WHERE ID = 1 FOR UPDATE;
-- Do work here
COMMIT TRANSACTION;
```
---

## Q40: Can you explain CSDL, SSDL and MSL sections in an EDMX file?
CSDL (Conceptual Schema Definition Language), SSDL (Store Schema Definition Language), and MSL (Mapping Specification Language) are sections of an EDMX file that together define the model, database, and the mapping between them in Entity Framework. CSDL describes the conceptual model, including entities, relationships, and properties as they appear in the application. SSDL defines the storage model, mapping entities and relationships to tables, columns, and constraints in the database. MSL maps the CSDL and SSDL, establishing the correlation between the conceptual entities and their storage representations. These sections enable EF to bridge application models with underlying databases.

```xml
<!-- Example snippet of EDMX file -->
<Schema Namespace="MyModel" xmlns="http://schemas.microsoft.com/ado/2008/09/edm">
    <!-- CSDL -->
    <EntityType Name="MyEntity">
        <Key>
            <PropertyRef Name="Id" />
        </Key>
        <Property Name="Id" Type="Int32" Nullable="false" />
    </EntityType>
</Schema>
<Schema Namespace="MyStore" xmlns="http://schemas.microsoft.com/ado/2009/02/edm/ssdl">
    <!-- SSDL -->
    <EntityType Name="MyTable">
        <Key>
            <PropertyRef Name="Id" />
        </Key>
        <Property Name="Id" Type="int" Nullable="false" StoreGeneratedPattern="Identity" />
    </EntityType>
</Schema>
-- MSL defines mapping -->
```
---

# Senior

## Q41: What types of system generated messages do you know?
System-generated messages typically occur in the context of exceptions, logs, or operational notifications within applications. In .NET applications, common system-generated messages include exceptions like `NullReferenceException`, `InvalidOperationException`, and `SqlException`. Logs may contain informational, warning, error, and critical messages generated by logging frameworks such as Serilog or NLog. In the context of database operations with Entity Framework, messages can be generated during data validation failures or model validation errors. Additionally, you might encounter messages during query execution, such as constraint violations or timeout exceptions.

---
## Q42: How can you enhance the performance of Entity Framework?
To enhance Entity Framework performance, use strategies such as disabling change tracking for read-only operations using `.AsNoTracking()`, which reduces overhead when tracking changes. Optimize queries by selecting only the required columns using projections with `.Select()`. Use indexing in the database to improve query execution time. Batch command executions and minimize database round trips by using methods like `AddRange()` and `RemoveRange()`. Implement caching strategies for frequently accessed data and use compiled queries to reduce parsing times. Also, consider eager loading related entities to minimize the number of database calls.

```csharp
using (var context = new MyDbContext())
{
    var data = context.Entities.AsNoTracking()
                 .Where(e => e.IsActive)
                 .Select(e => new { e.Id, e.Name })
                 .ToList();
}
```

---
## Q43: What is faster - ADO.NET or ADO.NET Entity Framework?
ADO.NET is generally faster than Entity Framework for raw data access because it provides direct access to the database and allows fine-grained control over SQL execution and data operations. Since ADO.NET operates at a lower abstraction level, it avoids the overhead associated with ORM functionalities like change tracking, lazy loading, and object materialization. However, Entity Framework offers significant productivity benefits through its high-level data access patterns, LINQ support, and automated model management, which might outweigh raw performance needs depending on the project requirements.

---
## Q44: What is the difference between POCO, Code First, and simple EF approach?
POCO (Plain Old CLR Object) classes are simple objects used to decouple domain model from database-specific concerns. The Code First approach uses POCOs to define the model classes, allowing developers to focus on the domain model and handle database schema creation through migrations. The simple EF approach, often described as "Database First" or "Model First," relies on generating database schema or model diagrammatically via design tools or existing databases. Code First provides more flexibility in evolving designs, whereas the simple EF approach is beneficial when modeling an existing, complex schema.

---
## Q45: What is the difference between ObjectContext and DbContext?
`ObjectContext` is the original class used in Entity Framework to manage database operations and track changes in the entities. It is more complex and often requires more configuration. `DbContext` is a simplified API introduced in Entity Framework 4.1, offering a more lightweight and easier-to-use interface. It streamlines common tasks and integrates seamlessly with modern .NET features like asynchronous operations and dependency injection. `DbContext` is typically preferred for new projects due to its ease of use and improvements in performance and maintainability.

---
## Q46: What is the difference between Code First, Model First, and Database First?
The "Code First" approach allows developers to define their database schema using C# classes and then generate the database from the code. "Model First" involves defining the model visually using a designer, which can then generate database scripts. "Database First" is used when starting with an existing database, generating the data model based on the database schema. Code First is useful for projects where the domain model drives design, Model First offers a visual design surface, and Database First is advantageous when integrating with legacy databases.

```csharp
// Code First Example
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}

// In the DbContext:
public DbSet<Product> Products { get; set; }
```

---

# Expert

## Q47: What difference does .AsNoTracking() make?

`AsNoTracking()` is a method in Entity Framework that allows you to query entities without tracking them in the context. This improves performance because it avoids the overhead of change tracking, especially useful in read-only scenarios where no updates to the context are needed. When entities are tracked, EF monitors any changes made to them so that it can persist those changes to the database on `SaveChanges()`. In contrast, the entities retrieved with `AsNoTracking()` are not monitored, leading to better performance for read operations. However, this means that any changes made to these entities will not be automatically saved unless explicitly attached to the context. `AsNoTracking()` is particularly beneficial in applications that handle large data retrieval operations.

```csharp
using (var context = new MyDbContext())
{
    var products = context.Products.AsNoTracking().ToList();
}
```
---

## Q48: What are the advantages and disadvantages of creating a Global Entities Context for the application (i.e. one static instance)?

Creating a global static instance of a DbContext can lead to several issues. The primary disadvantage is thread safety; DbContext is not thread-safe, so using it across multiple requests or threads can cause unexpected behavior or data corruption. Additionally, a long-lived context can lead to memory leaks because it holds onto more objects for longer periods, consuming more memory. This global context can also get outdated if the database schema changes during its lifecycle. One advantage could be reduced overhead from context re-initialization in applications with infrequent reads/writes, but this is rarely worth the risks mentioned. Typically, it's advisable to use a separate DbContext instance per request or operation to ensure thread safety and resource efficiency.

```csharp
public static class DbContextManager
{
    public static MyDbContext Context { get; } = new MyDbContext();
}
```
---

## Q49: What is client wins and store wins mode in Entity Framework concurrency?

Client wins and store wins are two strategies for resolving concurrency conflicts in Entity Framework. In client wins mode, changes made by the client's context override those in the database when a conflict occurs, meaning that the client’s version of the entity is saved. Store wins mode, on the other hand, keeps the database values intact whenever a conflict is detected, and the client’s changes are discarded. These modes come into play when using Optimistic Concurrency, where conflicts are detected but not prevented. The choice between client wins and store wins depends on the application's requirements regarding data integrity and user experience.

```csharp
try
{
    context.SaveChanges();
}
catch (DbUpdateConcurrencyException)
{
    foreach (var entry in context.ChangeTracker.Entries())
    {
        if (entry.State == EntityState.Modified)
        {
            var databaseValues = entry.GetDatabaseValues();
            entry.OriginalValues.SetValues(databaseValues); // Store wins
        }
    }
}
```
---

## Q50: What is the difference between Automatic Migration vs Code-Base Migration?

Automatic Migrations in Entity Framework simplify the process of updating the database schema to match the model with minimal code involvement, automatically detecting changes and applying them. However, it provides less control over the exact changes and might not handle complex schema changes or data transformations. Code-Based Migrations offer more control and transparency, as changes are explicitly defined in migration files, allowing for complex restructuring and custom scripts during migration. With Code-Based Migrations, developers gain the flexibility to review, modify, and plan database changes, ensuring fine-grained management of schema evolution.

```csharp
Add-Migration InitialCreate
Update-Database
```
---

## Q51: When would you use SaveChanges(false) + AcceptAllChanges()?

You would use `SaveChanges(false) + AcceptAllChanges()` in scenarios where you need to manually control the acceptance of changes in the context after saving them to the database. Calling `SaveChanges(false)` commits the changes to the database but does not reset the change tracker, allowing for transactions where you might retry saving changes if something fails initially. `AcceptAllChanges()` follows to reset the change tracker manually after ensuring a successful database transaction. This pattern is beneficial in handling partial failures, long-running operations, or custom transaction scopes where precise control over change tracking is required.

```csharp
using (var context = new MyDbContext())
{
    try
    {
        context.SaveChanges(false);
        // Perform additional operations if needed
        context.AcceptAllChanges();
    }
    catch
    {
        // Handle exceptions and potential retries
    }
}
```
---

## Q52: What's the difference between .SaveChanges() and .AcceptAllChanges()?

`SaveChanges()` persists all changes made in the context to the database and automatically calls `AcceptAllChanges()` afterward, which resets the change tracker and clears the context's state. On the other hand, `AcceptAllChanges()` is a standalone method used to manually reset the change tracker without performing a database commit. This distinction allows developers to control when the context's state is cleared separately from when changes are saved, providing greater flexibility especially in advanced transaction scenarios or when implementing a custom save logic.

```csharp
context.SaveChanges(); // Saves and accepts changes
// VS
context.SaveChanges(false); // Saves without accepting
context.AcceptAllChanges(); // Accepts manually
```
---

## Q53: Can I use Entity Framework 6 in .Net Core?

Yes, you can use Entity Framework 6 in a .NET Core application, but it requires specific configurations. EF6 is primarily designed for .NET Framework and might not support all .NET Core features, but certain projects have successfully integrated it by targeting .NET Standard. It's important to note that for full compatibility with .NET Core features, Entity Framework Core (EF Core) is recommended as it is specifically optimized for .NET Core environments and provides better performance, lightweight models, and more advanced capabilities such as shadow properties, alternate keys, and batch updates.

---

## Q54: How can we do pessimistic locking in Entity Framework?

Pessimistic locking can be implemented in Entity Framework using database transactions with explicit locking hints. Though EF primarily supports Optimistic Concurrency, you can use raw SQL queries with `DbContext.Database.ExecuteSqlCommand` to issue `SELECT ... FOR UPDATE` or similar SQL statements, locking the rows until the transaction completes. This approach ensures that data is locked for the duration of the transaction, preventing other transactions from modifying the locked data. However, it tightly couples your code to the specific SQL dialect of your database and can impact performance and scalability.

```csharp
using (var transaction = context.Database.BeginTransaction())
{
    context.Database.ExecuteSqlCommand("SELECT * FROM Products WITH (UPDLOCK) WHERE ProductId = 1");
    // Perform update operations here
    transaction.Commit();
}
```
---