# Entry

## Q1: Explain what is LINQ? Why is it required?
LINQ (Language Integrated Query) is a set of features in .NET that provides query capabilities directly in C# and VB.NET languages. It allows developers to query collections, XML, databases, and other data sources using a unified and strongly-typed syntax similar to SQL. LINQ is required because it simplifies complex querying tasks, enables compile-time checking, and promotes code readability and maintainability. With LINQ, queries can be written directly in code, eliminating the need for multiple query languages for different data sources, and reducing the risks of run-time errors.

```csharp
var numbers = new int[] { 1, 2, 3, 4, 5 };
var evenNumbers = numbers.Where(n => n % 2 == 0).ToList();
```
---

## Q2: What are the types of LINQ?
LINQ can be categorized into several types based on the data source it queries:
- LINQ to Objects: Queries in-memory collections like arrays, lists, etc.
- LINQ to SQL: Enables querying of Microsoft SQL Server databases using strongly-typed objects.
- LINQ to Entities: Works with the Entity Framework for querying relational data as entity objects.
- LINQ to XML: Queries XML data.
- LINQ to DataSet: Allows querying DataSets and DataTables.
- LINQ to JSON (with libraries like Newtonsoft.Json): For querying JSON structures.
Each type provides a consistent query experience while abstracting source-specific operations.

```csharp
// LINQ to Objects
var nums = new List<int> { 1, 2, 3 };
var result = nums.Where(x => x > 1);

// LINQ to XML
var xml = XElement.Parse("<root><item>1</item></root>");
var items = from el in xml.Elements() select el.Value;
```
---

## Q3: What are Anonymous Types?
Anonymous types, introduced in C# 3.0, are simple class types created on the fly without explicitly defining a class in code. They are used mainly to encapsulate a set of read-only properties into a single object, particularly useful in LINQ queries where temporary groupings or projections are needed. Anonymous types are defined using the `new` keyword followed by an object initializer without specifying the class name.

```csharp
var person = new { Name = "Alice", Age = 30 };
Console.WriteLine(person.Name); // Outputs: Alice
```
---

# Junior

## Q4: Mention what is the role of DataContext classes in LINQ?
The `DataContext` class acts as the main conduit between a LINQ-enabled data source and the application. It manages entity objects during run time, provides methods to query and submit changes, and keeps track of object states. It translates LINQ queries into SQL queries (if using LINQ to SQL) and executes them on the database. Each table in the database is typically represented as a property of the DataContext.

```csharp
public class MyDataContext : DataContext
{
    public Table<Customer> Customers;
}
```
---

## Q5: What are Extension Methods?
Extension methods are static methods that allow you to add new methods to existing types without modifying their source code or using inheritance. They are defined in static classes and the first parameter is preceded by the `this` modifier, specifying the type being extended. Extension methods are widely used by LINQ for providing query operators to `IEnumerable<T>` and other types.

```csharp
public static class Extensions
{
    public static bool IsEven(this int value) => value % 2 == 0;
}
int number = 4;
bool result = number.IsEven(); // true
```
---

## Q6: Explain why SELECT clause comes after FROM clause in LINQ?
In LINQ query expressions, the `SELECT` clause comes after the `FROM` clause to align with the flow of data and the C# language syntax. It enables defining the range variable and the data source before projecting the desired results. This syntax is similar to SQL yet more natural for code execution flow, promoting readability and clarity for developers.

```csharp
var query = from n in numbers
            where n > 2
            select n * 2;
```
---

## Q7: Explain what is LINQ to Objects?
LINQ to Objects refers to the usage of LINQ queries against in-memory collections like arrays, lists, or any type implementing `IEnumerable<T>`. It allows querying and manipulating data from these sources using a consistent query syntax, without any need for database or external data providers. LINQ to Objects supports rich filtering, projection, sorting, and aggregation, all performed in-memory.

```csharp
List<int> nums = new List<int> { 1, 2, 3, 4 };
var evenNums = nums.Where(n => n % 2 == 0);
```
---

## Q8: Explain what is the purpose of LINQ providers in LINQ?
LINQ providers are the components that interpret LINQ queries for different data sources. Each provider translates LINQ expressions into commands specific to its data source—such as SQL queries for databases, or XPath queries for XML. The provider handles query translation, execution, and result mapping, allowing developers to write consistent queries regardless of the underlying source.

```csharp
// Example using LINQ to XML provider
XDocument doc = XDocument.Parse("<root><val>1</val></root>");
var values = from v in doc.Descendants("val") select v.Value;
```
---

## Q9: Explain how LINQ is useful than Stored Procedures?
LINQ offers several advantages over stored procedures:
- Strongly-typed queries with compile-time checking.
- Improved readability and maintainability embedded in application code.
- Easier refactoring and debugging since queries are part of the application.
- No need for context switching between SQL and application code.
- Portability across different data storages.
However, stored procedures may be preferable for complex operations, better security, or performance in some scenarios.

```csharp
var products = dbContext.Products.Where(p => p.Price > 100).ToList();
```
---

## Q10: In LINQ how will you find the index of the element using where() with Lambda Expressions?
To find the index of a specific element using LINQ, you can use the `Select` method to project both the value and its index, then filter using `Where`. Finally, select the index.

```csharp
var list = new List<int> { 10, 20, 30 };
var index = list.Select((val, idx) => new { val, idx })
                .Where(x => x.val == 20)
                .Select(x => x.idx)
                .FirstOrDefault(); // index = 1
```
---

## Q11: What is Anonymous function?
An anonymous function is a method in C# without a name, created with either the `delegate` keyword or lambda expressions. Such functions are used for in-place, short-lived operations like event handlers or LINQ queries. They provide flexibility for small, self-contained logic where a full method would be overkill.

```csharp
Func<int, int, int> sum = delegate(int a, int b) { return a + b; };
// Or using lambda:
Func<int, int, int> lambdaSum = (a, b) => a + b;
```
---

## Q12: List out the three main components of LINQ?
The three main components of LINQ are:
- **Standard Query Operators**: Set of extension methods for querying collections.
- **Query Syntax (Language Extensions)**: Keywords like `from`, `where`, `select` integrated into C# or VB.NET.
- **LINQ Providers**: Components that translate LINQ queries for specific data sources (e.g., LINQ to SQL, LINQ to XML).

```csharp
var query = from n in numbers
            where n > 5
            select n;
```
---

## Q13: What is LINQ in C#?
LINQ (Language Integrated Query) in C# allows writing complex queries to retrieve, filter, order, and project information from various data sources like collections, XML, or databases, directly within code using a consistent syntax. It eliminates the need for language-specific querying APIs and provides compile-time type-checking, IntelliSense support, and easier debugging and maintenance.

```csharp
var highScores = from score in scores
                 where score > 80
                 select score;
```
---

# Mid

## Q14: What is the difference between First() and Take(1)?
`First()` returns the first element in a sequence, throwing an exception if the sequence is empty. `Take(1)` returns the first element as a collection (of one item) or an empty collection if the sequence is empty. Use `First()` when you need a single value, and `Take(1)` if you want to further process a one-item sequence or avoid exceptions with empty sources.

```csharp
var firstVal = numbers.First();         // Returns first element or throws if empty
var firstAsList = numbers.Take(1).ToList(); // Returns a list with one element, or empty list
```
---

## Q15: Explain what are LINQ compiled queries?
LINQ compiled queries are pre-compiled representations of LINQ queries, often used with LINQ to SQL or Entity Framework. Since normal LINQ queries are parsed and translated to SQL every time they are executed, compiled queries improve performance by compiling the query once and reusing it multiple times with different parameters, reducing repeated translation overhead.

```csharp
var query = CompiledQuery.Compile((MyDataContext db, int id) =>
    db.Users.Where(u => u.ID == id));
```
---

## Q16: Explain what is Lambda Expressions in LINQ?
Lambda expressions are concise ways to represent anonymous methods. In LINQ, they are heavily used for expressing predicates and selection logic in query methods like `Where` or `Select`. A lambda expression has syntax like `(parameters) => expression`. It increases readability and eliminates boilerplate code compared to anonymous methods.

```csharp
List<int> nums = new List<int> { 1, 2, 3 };
var evens = nums.Where(n => n % 2 == 0);
```
---

## Q17: What is Expression Trees and how they used in LINQ?
Expression trees are data structures that represent code in a tree-like format, where each node is an expression (like a method call or binary operation). In LINQ, expression trees allow providers (like LINQ to SQL) to inspect, translate, and execute queries against external sources. Extension methods accepting `Expression<Func<T, bool>>` build these trees, enabling providers to generate query-specific code like SQL.

```csharp
Expression<Func<int, bool>> isEven = x => x % 2 == 0;
// Providers can parse isEven and translate it to SQL where applicable.
```
---

## Q18: Could you compare Entity Framework vs LINQ to SQL vs ADO.NET with stored procedures?
- **Entity Framework (EF)**: Rich, modern ORM supporting multiple database engines, complex mapping, lazy/eager loading, and advanced change tracking. Supports both code-first and model-first approaches.
- **LINQ to SQL**: Lightweight ORM limited to SQL Server, supports basic object-relational mapping, less flexible than EF, but faster and simpler for small projects.
- **ADO.NET with Stored Procedures**: Low-level, requires manual mapping between data and objects. Offers best performance and full control over SQL execution, but lacks the abstraction and productivity of ORM tools.
EF is best for complex, scalable apps; LINQ to SQL for smaller, SQL Server-specific projects; ADO.NET for maximum performance and control.

```csharp
// Entity Framework
var user = dbContext.Users.Where(u => u.Name == "Bob").FirstOrDefault();

// LINQ to SQL
var user = db.Users.Where(u => u.Name == "Bob").FirstOrDefault();

// ADO.NET with SP
using (SqlCommand cmd = new SqlCommand("GetUser", conn)) {
    cmd.CommandType = CommandType.StoredProcedure;
    // ...
}
```
---

## Q19: When trying to decide between using the Entity Framework and LINQ to SQL as an ORM, what's the difference?
Entity Framework (EF) is more feature-rich than LINQ to SQL:
- EF supports multiple database providers, complex models, and flexible mapping (inheritance, many-to-many, etc.).
- LINQ to SQL is limited to SQL Server and supports only one-to-one table-to-class mapping.
- EF provides better support for migrations, complex domain models, and larger projects.
- LINQ to SQL is lightweight, simpler, with less overhead, and may suit small SQL Server-specific apps.
EF is recommended for larger, complex apps or multi-database support; LINQ to SQL for smaller, quick-prototyping apps on SQL Server.

```csharp
// EF - supports multiple DBs
var users = dbContext.Users.ToList();

// LINQ to SQL - only SQL Server
var users = db.Users.ToList();
```
---

## Q20: Could you explain what is the exact difference between deferred execution and Lazy evaluation in C#?
**Deferred Execution** is when execution of a query is delayed until its results are actually enumerated. In LINQ, queries like `Where` or `Select` are not run until you iterate over them.
**Lazy Evaluation** is a broader programming concept where an object or value is initialized or computed only at the point it is first needed.
In C#, deferred execution is often implemented using lazy evaluation under the hood. However, lazy evaluation can be applied to any value or object (e.g., via `Lazy<T>`), while deferred execution refers specifically to how LINQ or IEnumerable queries are executed.

```csharp
// Deferred execution in LINQ
var query = numbers.Where(x => x > 10); // Query is not run yet
foreach(var n in query) { ... }          // Now it runs

// Lazy evaluation with Lazy<T>
Lazy<int> lazyVal = new Lazy<int>(() => ExpensiveOperation());
```
---

## Q21: Define what is let clause?

The `let` clause in LINQ is used to create a new range variable and store the result of a sub-expression in a query, making queries more readable and enabling reuse within query expressions. It improves readability and performance when the same value is computed in multiple query parts. With `let`, you avoid repeating expressions and can optimize evaluation, especially when expensive operations or function calls are involved. It's available only in query syntax, not in method syntax, though similar results can be achieved using the `Select` extension method with anonymous types.

```csharp
var numbers = new[] { 1, 2, 3, 4, 5 };
var query = from n in numbers
            let square = n * n
            where square > 10
            select square;
// Output: 16, 25
```
---

## Q22: Explain how standard query operators useful in LINQ?

Standard Query Operators are built-in methods that form the core API of LINQ and operate on sequences (objects implementing IEnumerable/IQueryable). These operators provide methods to filter, project, aggregate, sort, join, and group data, allowing complex queries with readable and concise syntax. Examples include `Where` for filtering, `Select` for projection, `OrderBy` for sorting, and `GroupBy` for grouping data. These operators can be used with method or query syntax and can be chained to create powerful query compositions. Internally, some work with deferred execution for efficiency.

```csharp
var names = new[] { "Bob", "Alice", "Eve" };
var filtered = names.Where(n => n.StartsWith("A")).OrderBy(n => n);
// Output: Alice
```
---

## Q23: When to use First() and when to use FirstOrDefault() with LINQ?

Use `First()` when you expect at least one element that matches the condition; otherwise it will throw an `InvalidOperationException` if the sequence is empty. Use `FirstOrDefault()` when the sequence might be empty: it returns the default value (null for reference types, zero for numeric types) instead of throwing an exception. `First()` is suitable when a missing item should be considered an error, while `FirstOrDefault()` is useful for optional matches where you want to handle possible absence gracefully.

```csharp
var nums = new int[] { 1, 2, 3 };
var firstEven = nums.First(n => n % 2 == 0);       // Returns 2
var empty = new int[] { };
var orDefault = empty.FirstOrDefault();            // Returns 0 (default of int)
```
---

## Q24: Explain what is the difference between Skip() and SkipWhile() extension method?

`Skip(count)` bypasses a specified number of elements, always ignoring the first `count` elements regardless of their values. `SkipWhile(predicate)` skips elements as long as the given predicate is true, and then returns all remaining elements (even if the predicate would match again). This means `SkipWhile` is dependent on the data, while `Skip` is purely index-based.

```csharp
var list = new[] { 1, 2, 3, 2, 1, 4 };
var skipTwo = list.Skip(2);           // {3, 2, 1, 4}
var skipWhile = list.SkipWhile(x => x < 3); // {3, 2, 1, 4}
```
---

## Q25: Explain the difference between Select and Where

`Select` projects each element of a sequence into a new form, transforming data, while `Where` filters elements based on a predicate, returning only elements that satisfy the given condition. `Select` is used when you want to change the shape or content of the returned elements, whereas `Where` simply includes or excludes elements from the sequence.

```csharp
var nums = new[] { 1, 2, 3 };
var squares = nums.Select(n => n * n);   // {1, 4, 9}
var evens = nums.Where(n => n % 2 == 0); // {2}
```
---

## Q26: Name some advantages of LINQ over Stored Procedures

LINQ offers type safety, compile-time syntax checking, and IntelliSense support in Visual Studio. Queries are easier to maintain because they are often written in the same language (C#) as application logic, resulting in better readability and maintainability. Refactoring is simpler, unit testing is more seamless, and complex object mapping (including navigation of related entities) is easier to express. LINQ queries are database-agnostic, allowing you to change providers or backends with minimal code changes, whereas stored procedures are database-specific.

```csharp
// Query embedded in C#, type-safe, no external dependency
var result = context.Products.Where(p => p.Price > 20).ToList();
```
---

# Senior

## Q27: When should I use a CompiledQuery?

You should use a CompiledQuery in scenarios where the same LINQ to SQL or Entity Framework query is executed multiple times with different parameters. It avoids the repeated cost of parsing and compiling the query expression by caching the execution plan. This is especially useful for high-performance applications or those under heavy load, where the efficiency gain from reusing query plans is significant. For ad-hoc or less frequent queries, CompiledQuery is unnecessary and may add complexity.

```csharp
Func<MyDataContext, decimal, IQueryable<Product>> query =
   CompiledQuery.Compile((MyDataContext ctx, decimal minPrice) =>
      ctx.Products.Where(p => p.Price >= minPrice));
```
---

## Q28: What is an equivalent to the let keyword in chained LINQ extension method calls?

The equivalent of `let` in method syntax is to use `Select` to introduce an anonymous type carrying the new value along with the original element. This allows intermediate results to be reused in later chained operations, similar to how `let` works in query syntax.

```csharp
var query = numbers
    .Select(n => new { n, Square = n * n })
    .Where(x => x.Square > 10)
    .Select(x => x.Square);
```
---

## Q29: Can you provide a concise distinction between anonymous method and lambda expressions?

Anonymous methods and lambda expressions are both ways to declare inline delegates. Anonymous methods use the `delegate` keyword and were introduced in C# 2.0; lambda expressions, introduced in C# 3.0, are more concise and allow inferred parameter types and expression bodies. Lambdas also support expression trees, making them more flexible and powerful, especially with LINQ.

```csharp
Action a1 = delegate(int x) { Console.WriteLine(x); }; // Anonymous method
Action<int> a2 = x => Console.WriteLine(x);            // Lambda expression
```
---

## Q30: What is the difference between returning IQueryable<T> vs. IEnumerable<T>?

`IQueryable<T>` represents a query that can be translated to an underlying data source, enabling deferred execution and remote query composition (e.g., database queries). `IEnumerable<T>`, on the other hand, represents an in-memory collection and queries will be executed in memory, not translated to the data source. Returning `IQueryable<T>` allows further filtering before execution, whereas returning `IEnumerable<T>` executes the query immediately, bringing all results to memory.

```csharp
public IQueryable<Product> GetQueryableProducts() => db.Products;
public IEnumerable<Product> GetAllProducts() => db.Products.ToList();
```
---

# Expert

## Q31: What are the benefits of a Deferred Execution in LINQ?

Deferred execution means that the query isn't executed when defined, but when the data is enumerated. Benefits include improved performance, as queries are only executed when needed; up-to-date results, as the underlying data can change between query declaration and execution; lower memory use, as data is not unnecessarily materialized; and composability, allowing queries to be built incrementally and combined before execution.

```csharp
var query = list.Where(x => x > 10); // Not executed here
foreach(var n in query) { ... }      // Executed here
```
---

## Q32: Why use AsEnumerable() rather than casting to IEnumerable<T>?

`AsEnumerable()` is preferred because it explicitly signals a switch from query-provider-supported operations to in-memory LINQ-to-Objects operations. It also handles cases where the query provider does not natively implement `IEnumerable<T>`. Direct casting can fail if the underlying object does not implement the interface, while `AsEnumerable()` always returns a valid `IEnumerable<T>`, ensuring method chaining works safely.

```csharp
var result = db.Products
    .AsEnumerable()           // Switch from DB queries to in-memory
    .Where(p => SomeMethod(p)); 
```
---

## Q33: What is the difference between Select and SelectMany?

`Select` projects each element into a new form and results in a sequence of sequences if the selector returns collections. `SelectMany` flattens those inner sequences into a single sequence, commonly used when each item can produce multiple results, and you want to process them as a flat sequence.

```csharp
var numbers = new[] { new[] { 1,2 }, new[] { 3,4 } };
var select = numbers.Select(arr => arr);        // Sequence of arrays
var selectMany = numbers.SelectMany(arr => arr); // Flattened: 1,2,3,4
```
---

## Q34: Name some disadvantages of LINQ over Stored Procedures

LINQ queries may have performance overhead due to expression parsing and translation, and may generate less efficient SQL than a finely-tuned stored procedure. Complex queries can become hard to maintain in application code, and LINQ lacks features like advanced transaction management, security, or fine-grained tuning of execution plans available in stored procedures. Also, stored procedures can encapsulate business logic on the DB side, reducing network traffic for bulk operations.

```csharp
// LINQ may generate SQL that's less efficient than equivalent stored procedure
var result = context.Orders.Where(o => o.Total > 1000).ToList();
```
---