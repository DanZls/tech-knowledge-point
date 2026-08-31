# Questions: C#, .Net Core, LINQ (Web Development)


## 1. Language & Type System

What is C#?
What is an object?
What is the difference between a class and a structure?
What is the difference between value types and reference types?
What are the different types of classes in C#?
What is an abstract class?
What is the difference between an interface and an abstract class?
Why are interface members implicitly public, and can that be changed?
What are generics in C#?
What is boxing and unboxing?
What happens when you box or unbox a nullable value type?
What are nullable value types, and how do they differ from nullable reference types?
What problem do nullable reference types (C# 8+) solve, and how does the compiler enforce them?
What is the null-coalescing operator (`??`) used for, and how does it differ from the null-conditional operator (`?.`)?
What is the difference between `string` and `StringBuilder`?
What is the difference between `is` and `as` operators?
What is an indexer in C#?
What is the difference between `decimal`, `float`, and `double`?
What is a partial class, and when would you use one?
What is a namespace, and why is it used?
What is an enum in C#, and how is its underlying storage represented?
What is the difference between `var` and an explicitly typed declaration?
What is pattern matching in C#, and what kinds of patterns can you match on (type, property, relational)?
What are records, and what problem were they introduced to solve?


## 2. Object-Oriented Programming

How is encapsulation implemented in C#?
What is the difference between overloading and overriding?
What are the different ways a method can be overloaded?
What is the difference between a virtual method and an abstract method?
How can you prevent a class from being inherited?
What is a sealed class used for?
Can multiple inheritance be implemented in C#?
What is the difference between `Equals()` and the `==` operator?
What is the difference between method hiding (`new`) and method overriding (`override`)?
Can a constructor be private, and why would you make one private?
What is constructor chaining in C#?
What is a static constructor, and what is it used for?
Why does a static class need no object, and can a static class have only static members?
Can a non-static class have static members?
What is the difference between an interface, an abstract class, a sealed class, a static class, and a partial class?
Why can't an abstract class be sealed or static?
Can interfaces define static members, and how does this differ from a regular static method?
When should you use an abstract class instead of an interface with default/extension methods?
What is the difference between `init`-only property setters and regular setters, and what problem do they solve?


## 3. Memory, Exceptions & Resource Management

What is managed vs unmanaged code?
How is exception handling implemented in C#?
Why use a `finally` block?
Can multiple `catch` blocks execute for a single thrown exception?
Is there a way to handle multiple exception types in one `catch` block without duplicating logic?
What is the difference between `throw` and `throw ex`?
What is a finalizer in C#, and how does its syntax (`~ClassName()`) relate to `Object.Finalize()`?
What is the difference between a finalizer and `Dispose()`?
What is the purpose of the `IDisposable` interface, and how does the `using` statement rely on it?
When, if ever, should a class define a finalizer?
Why might a class's finalizer never run, or run later than expected?
What is the difference between `const` and `readonly`?
What is the `volatile` keyword used for?
Why use the `lock` statement in C#, and what problem does it prevent?
Why is deriving custom exceptions from `System.ApplicationException` no longer recommended?
What is serialization, and why is it used?
What is the difference between a `StackOverflowException` and an `OutOfMemoryException`?


## 4. Delegates, Lambdas & Functional Features

What is a delegate?
What is a multicast delegate?
What is the difference between `Func`, `Action`, and `Predicate`?
What is a lambda expression?
What is the difference between a lambda expression and a delegate type?
What is an anonymous method, and how does it compare to a lambda expression?
What is an anonymous type in C#?
When would you choose to use delegates in C#?
What is the difference between using a `Func<string, string>` and defining a custom `delegate` type?


## 5. Advanced C# Concepts

What is reflection in C#?
What is the difference between early binding and late binding?
What are `dynamic` type variables, and how do they differ from `object`?
What is an extension method, and how is it used?
Can extension methods be added for a type you don't own, and what are the limitations?
What is operator overloading, and how is it implemented in C#?
What is the `yield` keyword used for, and how does it relate to iterator methods?
What is the difference between `Task` and `Thread`?
How does async/await work conceptually, and what does the compiler generate behind the scenes?
What is the difference between `Task` and `ValueTask`, and when would you use each?
What does `MemberwiseClone()` do?
What is the difference between a shallow copy and a deep copy?
What is a `WeakReference` in C#, and when is it useful?
What is marshalling, and why is it needed when interoperating with native code?
When should you use a `record` instead of a `class` or `struct`?
What is the difference between `System.Array.CopyTo()` and `System.Array.Clone()`?
What is a jagged array, and when is it preferred over a multidimensional array?
What is short-circuit evaluation, and is relying on it safe practice?
What is the scope of an `internal` member in a C# class?
What is the scope of a `protected internal` member versus a `private protected` member?
What are circular references, and what strategies exist to avoid or resolve them?
What is the use of conditional preprocessor directives in C#?
In how many ways can parameters be passed to a method?
What is the difference between `ref` and `out` parameters?
What does the `in` parameter modifier add compared to `ref` and `out`?
Can `this` be used within a static method or a static context?
What are the stages a C# program goes through from source code to execution?
What is the difference between a compile-time error and a run-time error?
What are `Span<T>` and `Memory<T>`, and what performance problem do they address?
What are top-level statements, and how do they change the structure of a C# program's entry point?


## 6. .NET Runtime & Platform Fundamentals
 
What is the CLR (Common Language Runtime)?
What core services does the CLR provide?
What is the CTS (Common Type System), and why does it matter for cross-language interoperability?
What is the CLS (Common Language Specification)?
What is MSIL/CIL, and what role does it play in .NET compilation?
What is a JIT compiler, and what problem does it solve?
What is Native AOT in modern .NET, and how does it differ from JIT compilation?
What benefits does Native AOT provide for startup time, memory footprint, and container image size, and what are its limitations (e.g. reduced reflection support)?
What is CoreCLR, and how does it relate to the unified .NET runtime used today?
What is garbage collection in .NET, and how do GC generations work?
Why might garbage collection introduce pauses in an application, and what factors influence this?
What is an unmanaged resource, and why does it require explicit cleanup?
What is the difference between an assembly, a process, and a thread?
What deployment models exist for a .NET application (framework-dependent, self-contained, single-file, Native AOT publish), and how do they trade off size against portability?
What is an IoC (Dependency Injection) container, and what problem does it solve?
What are the standard DI service lifetimes (Transient, Scoped, Singleton)?
When would you choose Transient vs Scoped vs Singleton for a service?
What issues can arise from injecting a shorter-lived service into a longer-lived one (a "captive dependency")?


## 7. LINQ
 
What is LINQ, and why was it introduced?
What are the different LINQ providers (LINQ to Objects, LINQ to Entities, LINQ to XML), and how do they differ?
What are the three main components involved in a LINQ query (data source, query, execution)?
What is LINQ to Objects?
What is the role of a LINQ provider in translating a query to its underlying data source?
How do extension methods enable LINQ's fluent, chainable query syntax?
What are anonymous types, and how are they commonly used with LINQ projections?
Why does the `select` clause come after the `from` clause in LINQ query syntax?
What is the difference between `Select` and `Where`?
What is the difference between `Select` and `SelectMany`?
What is the difference between `First()` and `Take(1)`?
When should you use `First()` versus `FirstOrDefault()`?
What is the difference between `Skip()` and `SkipWhile()`?
What is the `let` clause used for in LINQ query syntax, and what is its equivalent in method-chain syntax?
How do standard query operators (like `Where`, `OrderBy`, `GroupBy`) work together to build a query pipeline?
What are expression trees, and how does LINQ use them to translate queries for external providers?
What is deferred execution in LINQ, and how does it differ from lazy evaluation more generally?
What is the difference between `IEnumerable<T>` and `IQueryable<T>`?
Why would you call `AsEnumerable()` on an `IQueryable<T>` before applying further operations?
What problems do the newer LINQ methods `Index`, `CountBy`, and `AggregateBy` (added in .NET 9) solve compared to the older `Select`/`GroupBy`-based patterns?


## 8. Web Development (ASP.NET Core)
 
What are Minimal APIs, and how do they differ architecturally from the traditional MVC controller-based approach?
When would you choose Minimal APIs over a controller-based Web API project?
What constraints does Native AOT publishing place on an ASP.NET Core app (e.g. reduced support for reflection-based features)?
What is Blazor, and what problem does it solve for .NET developers building interactive web UIs?
What is the architectural difference between Blazor Server and Blazor WebAssembly rendering?
What is a Blazor Web App (the unified full-stack render-mode model), and how does it let you mix server and client rendering per component?
What is SignalR, and what problem does it solve for real-time web communication?
What is gRPC, and when would you choose it over a traditional REST/HTTP API?
What is the purpose of health check endpoints in a cloud-native web service?
What is output caching, and how does it differ conceptually from response caching?
What is the conceptual purpose of rate-limiting middleware in a web API?
What is OpenAPI, and how does ASP.NET Core generate API documentation directly from source?
What is .NET Aspire, and what problem does it solve for orchestrating and observing multi-project, cloud-native applications locally?
Why is containerizing an ASP.NET Core app a common practice, and how does Native AOT affect resulting image size and startup time?
What is the purpose of structured logging and distributed tracing (e.g. via OpenTelemetry) in a modern web service?
What is the difference between a traditional server-rendered app, a Single Page Application (SPA), and a hybrid model like Blazor's, in terms of where UI logic executes?

---
