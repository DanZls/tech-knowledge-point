# Clean Architecture


## Contents
- [What do you understand by Clean Architecture approach?](#what-do-you-understand-by-clean-architecture-approach)
- [What is an Entity in Clean Architecture?](#what-is-an-entity-in-clean-architecture)
- [Explain the Data Flow in Clean Architecture](#explain-the-data-flow-in-clean-architecture)
- [How you pass data between modules where they have different models in Clean Architecture?](#how-you-pass-data-between-modules-where-they-have-different-models-in-clean-architecture)
- [What are Use Cases in Clean Architecture?](#what-are-use-cases-in-clean-architecture)
- [What is the role of the Controller in Clean Architecture?](#what-is-the-role-of-the-controller-in-clean-architecture)
- [What is the role of the Presenter in Clean Architecture?](#what-is-the-role-of-the-presenter-in-clean-architecture)
- [Explain the purpose of Clean Architecture Inner and Outer layers](#explain-the-purpose-of-clean-architecture-inner-and-outer-layers)
- [Explain what is Dependency Rule in Clean Architecture](#explain-what-is-dependency-rule-in-clean-architecture)
- [Explain what is Interface Segregation Principle (ISP) in Clean Architecture and what are some of its benefits?](#explain-what-is-interface-segregation-principle-isp-in-clean-architecture-and-what-are-some-of-its-benefits)
- [What do you mean by Clean Architecture is Screaming?](#what-do-you-mean-by-clean-architecture-is-screaming)
- [What is the difference between the Clean and the N-Tier Architectures?](#what-is-the-difference-between-the-clean-and-the-n-tier-architectures)
- [How shall we integrate DB Layer access in Clean Architecture?](#how-shall-we-integrate-db-layer-access-in-clean-architecture)
- [Where should I implement the external API calls logic in Clean Architecture?](#where-should-i-implement-the-external-api-calls-logic-in-clean-architecture)
- [Explain the control flow of a user interacting with Clean Architecture components?](#explain-the-control-flow-of-a-user-interacting-with-clean-architecture-components)
- [Compare Onion vs Clean vs Hexagonal Architectures](#compare-onion-vs-clean-vs-hexagonal-architectures)
- [What is the difference between Request/Response Models and Entities in Clean Architecture?](#what-is-the-difference-between-requestresponse-models-and-entities-in-clean-architecture)
- [How and where do you use transactions in the Clean Architecture?](#how-and-where-do-you-use-transactions-in-the-clean-architecture)

---


## What do you understand by Clean Architecture approach?
Clean Architecture, popularized by Robert C. Martin, organizes a .NET solution into concentric layers - Domain, Application, Infrastructure, and Presentation - where dependencies always point inward toward the business logic. The Domain layer holds Entities and business rules with zero external dependencies, the Application layer defines Use Cases and abstractions (interfaces), and Infrastructure implements those abstractions using EF Core, MSSQL, or Azure services. The Presentation layer (an ASP.NET Core Web API) only orchestrates HTTP requests and delegates work to the Application layer. This separation makes the core business logic independent of frameworks, databases, and UI, so you can swap MSSQL for another store or replace Azure Service Bus without touching business rules. It also greatly improves testability because the Domain and Application layers can be unit tested without spinning up a database or web server. In practice, this is implemented as separate class library projects (e.g. `MyApp.Domain`, `MyApp.Application`, `MyApp.Infrastructure`, `MyApp.WebApi`) with project references enforcing the dependency direction at compile time.

```csharp
// MyApp.Application depends only on MyApp.Domain
// MyApp.Infrastructure depends on MyApp.Application (implements its interfaces)
// MyApp.WebApi depends on MyApp.Application and MyApp.Infrastructure (for DI registration)
public interface IOrderRepository
{
    Task<Order> GetByIdAsync(Guid id);
}
```

---


## What is an Entity in Clean Architecture?
An Entity is a plain object living in the Domain layer that encapsulates enterprise-wide business rules and invariants, independent of any persistence or framework concerns. In a .NET solution, Entities are typically POCOs with private setters and behavior-rich methods, avoiding anemic models where logic leaks into services. Entities should not carry EF Core attributes like `[Table]` or `[Key]` directly if you want a pure Domain layer; instead, mapping is configured separately via Fluent API in the Infrastructure layer. They can raise Domain Events (e.g. `OrderPlacedEvent`) that are dispatched after a transaction commits, which integrates well with Azure Service Bus or MediatR-based pipelines. Keeping validation and invariants inside Entities (rather than in controllers or services) ensures the object can never exist in an invalid state. This is the innermost layer, so it has no dependency on the Application, Infrastructure, or Presentation layers.

```csharp
public class Order
{
    public Guid Id { get; private set; }
    public OrderStatus Status { get; private set; }

    public void MarkAsShipped()
    {
        if (Status != OrderStatus.Paid)
            throw new InvalidOperationException("Order must be paid before shipping.");
        Status = OrderStatus.Shipped;
    }
}
```

---


## Explain the Data Flow in Clean Architecture
A request enters through the Presentation layer (an ASP.NET Core controller or minimal API endpoint), which maps the HTTP request into an input model and forwards it to the Application layer, typically via a Mediator (MediatR) command or query. The Application layer's Use Case handler orchestrates business logic, calling Domain Entities and abstractions such as `IOrderRepository` or `IEmailSender`. These interfaces are implemented in the Infrastructure layer using EF Core against MSSQL, or SDKs for Azure Blob Storage, Service Bus, or Key Vault, and are injected via .NET's built-in DI container. The Use Case returns a Response/DTO back up through the Application layer to the Controller, which then maps it to an HTTP response (status code, JSON body). Data therefore flows inward as commands/queries and outward as responses, while dependencies always point inward - Infrastructure depends on Application abstractions, never the reverse. This inversion is what keeps the Domain and Application layers free of infrastructure concerns and easily testable in isolation.

```csharp
[ApiController]
[Route("api/orders")]
public class OrdersController : ControllerBase
{
    private readonly IMediator _mediator;
    public OrdersController(IMediator mediator) => _mediator = mediator;

    [HttpGet("{id}")]
    public async Task<IActionResult> Get(Guid id)
    {
        var result = await _mediator.Send(new GetOrderQuery(id));
        return Ok(result);
    }
}
```

---


## How you pass data between modules where they have different models in Clean Architecture?
When crossing layer boundaries, data is translated between models rather than sharing the same class across layers, to avoid leaking implementation details. Typically this is done with DTOs/Request-Response models at the Application boundary and mapping libraries like AutoMapper or Mapster to convert between Entities, EF Core entities, and API contracts. For example, a `CreateOrderRequest` from the API is mapped to a `CreateOrderCommand`, which the handler translates into an `Order` Entity; the persisted Entity is then mapped back to an `OrderResponse` DTO for the client. In distributed .NET systems on Azure, cross-service communication (via Service Bus messages or HTTP calls between microservices) uses versioned message/event contracts that are independent of each module's internal Domain model. Keeping explicit mapping boundaries prevents a change in the database schema or Domain model from silently breaking the public API contract. It also allows each module to evolve its internal model independently as long as the mapping contract is preserved.

```csharp
public class OrderProfile : Profile
{
    public OrderProfile()
    {
        CreateMap<CreateOrderCommand, Order>();
        CreateMap<Order, OrderResponse>();
    }
}
```

---


## What are Use Cases in Clean Architecture?
Use Cases (also called Interactors or Application Services) represent the application-specific business rules - the actions a user or system can perform, such as "PlaceOrder" or "CancelSubscription". In a .NET implementation, Use Cases are commonly modeled as MediatR `IRequestHandler<TCommand, TResponse>` classes living in the Application layer, one per operation, following the Single Responsibility Principle. Each Use Case orchestrates Domain Entities and calls Infrastructure abstractions (repositories, external services) through interfaces, without knowing whether the implementation uses MSSQL, Azure Cosmos DB, or a REST API. This makes Use Cases the primary place to enforce validation (often paired with FluentValidation), transaction boundaries, and Domain Event dispatching. Because Use Cases depend only on abstractions, they can be unit tested with mocked repositories (e.g. Moq or NSubstitute) without a real database. Structuring the Application layer this way also makes the codebase "screaming" its intent, since folder/class names describe business capabilities rather than technical layers.

```csharp
public class PlaceOrderCommand : IRequest<Guid> { public Guid CustomerId; public List<OrderLine> Lines; }

public class PlaceOrderHandler : IRequestHandler<PlaceOrderCommand, Guid>
{
    private readonly IOrderRepository _repository;
    public PlaceOrderHandler(IOrderRepository repository) => _repository = repository;

    public async Task<Guid> Handle(PlaceOrderCommand request, CancellationToken ct)
    {
        var order = Order.Create(request.CustomerId, request.Lines);
        await _repository.AddAsync(order, ct);
        return order.Id;
    }
}
```

---


## What is the role of the Controller in Clean Architecture?
The Controller sits in the Presentation layer and is the entry point that translates an external request (HTTP, gRPC, message queue trigger) into a call to a Use Case in the Application layer. In ASP.NET Core, a Controller (or a minimal API endpoint) validates the shape of the incoming request via model binding and `[ApiController]` automatic validation, then constructs a Command or Query object and passes it to the Mediator. It intentionally contains no business logic - its only responsibilities are request/response translation, authorization attribute checks, and HTTP status code selection. This keeps the Controller thin and framework-bound, meaning if you migrated from ASP.NET Core to Azure Functions HTTP triggers, only the Presentation layer would change while Application and Domain logic remain untouched. Controllers depend on Application layer abstractions (like `IMediator` or Use Case interfaces), never on Infrastructure implementations directly. This separation also simplifies integration testing using `WebApplicationFactory`, since you can substitute Infrastructure dependencies without touching Controller code.

```csharp
[HttpPost]
public async Task<IActionResult> Create([FromBody] CreateOrderRequest request)
{
    var orderId = await _mediator.Send(new PlaceOrderCommand(request.CustomerId, request.Lines));
    return CreatedAtAction(nameof(Get), new { id = orderId }, null);
}
```

---


## What is the role of the Presenter in Clean Architecture?
The Presenter is responsible for formatting the output of a Use Case into a representation suitable for the delivery mechanism, decoupling how data is structured internally from how it's displayed or serialized externally. In a typical .NET Web API, this role is often merged into the Controller or handled by a dedicated `IViewModelMapper`/response DTO, converting the Use Case's output model into the exact JSON shape, HAL/HATEOAS links, or ViewModel a client expects. Having a distinct Presenter becomes valuable when the same Use Case must serve multiple channels - for example, a REST API response versus a message published to Azure Service Bus versus a server-rendered Razor page - each requiring different formatting without duplicating business logic. The Presenter also can apply presentation-specific concerns like localization, pagination metadata, or hiding sensitive fields before the response leaves the system boundary. Because Presenters are Outer layer components, they can depend on Application layer output models but never leak formatting concerns back into Use Cases. Keeping this responsibility isolated makes it trivial to add a new client type without touching the Application layer.

```csharp
public class OrderPresenter
{
    public OrderResponse Present(Order order) =>
        new OrderResponse(order.Id, order.Status.ToString(), order.Total.ToString("C"));
}
```

---


## Explain the purpose of Clean Architecture Inner and Outer layers
The Inner layers (Domain and Application) contain the enterprise and application business rules and must remain free of any framework, database, or UI dependency - no references to EF Core, ASP.NET Core, or Azure SDKs are allowed there. The Outer layers (Infrastructure and Presentation) contain volatile, replaceable details: EF Core `DbContext` and repository implementations for MSSQL, Azure Blob/Queue/Service Bus clients, external HTTP integrations, and the ASP.NET Core Web API/Controllers. This separation exists because implementation details (databases, UI frameworks, cloud SDKs) change far more often than core business rules, so isolating them protects the stable core from churn. Outer layers depend on Inner layers via interfaces defined in the Application layer, and concrete implementations are wired up at startup using .NET's dependency injection container (`Program.cs`). For example, switching from MSSQL to Azure Cosmos DB only requires a new Infrastructure implementation of `IOrderRepository`, with zero changes to Domain or Application code. This layered separation is what enables long-term maintainability and lets teams work on different layers in parallel.

```csharp
// Program.cs - wiring an Outer layer implementation to an Inner layer abstraction
builder.Services.AddScoped<IOrderRepository, SqlOrderRepository>();
```

---


## Explain what is Dependency Rule in Clean Architecture
The Dependency Rule states that source code dependencies can only point inward - nothing in an inner layer can know anything about an outer layer. Concretely in a .NET solution, this means the `MyApp.Domain` project has no project references at all, `MyApp.Application` only references `MyApp.Domain`, and `MyApp.Infrastructure`/`MyApp.WebApi` reference `MyApp.Application` to implement its interfaces. When an inner layer needs a capability provided by an outer layer (e.g. saving to MSSQL), it defines an interface in the inner layer (e.g. `IOrderRepository` in Application) and the outer layer provides the implementation (e.g. `SqlOrderRepository` in Infrastructure) - this is the Dependency Inversion Principle applied at the architecture level. The rule is enforced at compile time through project reference direction, so violating it (e.g. Domain referencing Infrastructure) causes a build error, not just a code review comment. This guarantees the Domain and Application layers can be compiled, tested, and reused without any Infrastructure or Presentation code present. It's the central mechanism that makes Clean Architecture's promises of testability and framework independence achievable in practice.

```csharp
// Application (inner) defines the abstraction
public interface IOrderRepository { Task AddAsync(Order order, CancellationToken ct); }

// Infrastructure (outer) implements it, referencing Application, not the other way around
public class SqlOrderRepository : IOrderRepository
{
    private readonly AppDbContext _db;
    public SqlOrderRepository(AppDbContext db) => _db = db;
    public Task AddAsync(Order order, CancellationToken ct) => _db.Orders.AddAsync(order, ct).AsTask();
}
```

---


## Explain what is Interface Segregation Principle (ISP) in Clean Architecture and what are some of its benefits?
ISP states that clients should not be forced to depend on interfaces they don't use, meaning large, general-purpose interfaces should be split into smaller, role-specific ones. In Clean Architecture this is applied heavily at the Application layer boundary - instead of one fat `IOrderRepository` with dozens of methods, you define narrow interfaces like `IOrderReader` and `IOrderWriter`, or per-Use-Case interfaces such as `IPlaceOrderGateway`, so each Use Case only depends on the members it actually needs. In a .NET context this reduces coupling between Use Cases and Infrastructure, since a change to an unrelated method on a repository doesn't force recompilation or retesting of unrelated handlers. It also makes mocking dramatically simpler in unit tests (with Moq/NSubstitute), because a small interface requires fewer setups than a monolithic one. Applied to Azure integrations, ISP means defining a focused `INotificationSender` instead of a generic `IAzureServiceClient` that mixes Service Bus, Blob Storage, and Key Vault concerns. Overall, ISP improves modularity, testability, and makes the codebase easier to reason about and refactor safely.

```csharp
public interface IOrderReader { Task<Order> GetByIdAsync(Guid id); }
public interface IOrderWriter { Task AddAsync(Order order); }

public class SqlOrderRepository : IOrderReader, IOrderWriter { /* implements both */ }
```

---


## What do you mean by Clean Architecture is Screaming?
"Screaming Architecture" means that looking at the top-level folder/project structure of a solution should immediately communicate what the system does (e.g. "this is an Order Management system"), rather than what framework it uses (e.g. "this is an ASP.NET Core MVC app"). In a .NET solution this translates into organizing the `Application` layer by feature/Use Case folders - `Orders`, `Payments`, `Shipping` - each containing its Commands, Queries, and Handlers, instead of organizing by technical concern like `Controllers`, `Services`, `Repositories`. Framework details (ASP.NET Core, EF Core, Azure SDKs) are pushed to the outer, replaceable Infrastructure/Presentation layers and don't dominate the solution structure. This approach helps new developers and interviewers alike understand the business domain quickly just by browsing the folder tree, and it signals that the framework is a delivery mechanism, not the architecture itself. It's a natural consequence of following the Dependency Rule strictly, since business capabilities live in the Inner layers that are named and organized around the domain. Screaming Architecture also makes it easier to extract a bounded context into its own microservice later, since the feature folder already maps closely to a potential service boundary.

```
src/
  MyApp.Domain/
  MyApp.Application/
    Orders/
    Payments/
    Shipping/
  MyApp.Infrastructure/
  MyApp.WebApi/
```

---


## What is the difference between the Clean and the N-Tier Architectures?
Traditional N-Tier (layered) architecture organizes code by technical responsibility - Presentation, Business Logic Layer (BLL), Data Access Layer (DAL) - where dependencies typically flow top-down, and the Business layer often directly depends on the DAL, meaning it knows about MSSQL/EF Core specifics. Clean Architecture instead enforces the Dependency Rule so that the Business/Domain layer has zero dependency on the Data Access layer; instead, the DAL (Infrastructure) implements interfaces defined by the Business layer, inverting the dependency direction. This means in N-Tier, replacing MSSQL with Azure Cosmos DB often requires touching the BLL, whereas in Clean Architecture only the Infrastructure implementation changes. N-Tier also tends to group code by layer across the whole application, while Clean Architecture (following Screaming Architecture) groups Use Cases by business feature within the Application layer. Testability differs too - N-Tier's BLL is harder to unit test in isolation because it's often tightly coupled to concrete DAL classes, while Clean Architecture's Application layer can be tested with mocked interfaces alone. In short, N-Tier separates by technical layer with downward-only coupling awareness, while Clean Architecture separates by dependency direction with the Domain fully isolated from infrastructure concerns.

```csharp
// N-Tier: BLL directly depends on DAL implementation
public class OrderService { private readonly SqlOrderDal _dal; }

// Clean Architecture: Application depends on an abstraction, DAL implements it
public class PlaceOrderHandler { private readonly IOrderRepository _repository; }
```

---


## How shall we integrate DB Layer access in Clean Architecture?
Database access belongs in the Infrastructure layer, which implements repository interfaces defined in the Application layer, keeping EF Core's `DbContext`, MSSQL-specific SQL, and connection strings out of the Domain and Application code entirely. In practice, you create an `AppDbContext` in `MyApp.Infrastructure`, configure entity mappings with Fluent API (avoiding data annotations on Domain Entities), and implement `IOrderRepository` as `SqlOrderRepository` that wraps `DbContext` queries. Connection strings and MSSQL credentials are supplied via configuration (appsettings + Azure Key Vault/App Configuration in production), following 12-factor principles of externalized config. The Application layer's Use Cases call only the repository interface, so unit tests mock `IOrderRepository` while integration tests can spin up a real or in-memory/SQLite/Testcontainers MSSQL instance to validate the Infrastructure implementation. Transactions, connection pooling, and retry policies (e.g. `EnableRetryOnFailure` for transient Azure SQL faults) are also Infrastructure concerns configured in `DbContext` setup. This keeps the Domain/Application layers portable across relational or NoSQL stores as long as the repository contract is honored.

```csharp
public class AppDbContext : DbContext
{
    public DbSet<Order> Orders => Set<Order>();
    protected override void OnModelCreating(ModelBuilder modelBuilder) =>
        modelBuilder.ApplyConfigurationsFromAssembly(typeof(AppDbContext).Assembly);
}
```

---


## Where should I implement the external API calls logic in Clean Architecture?
External API integrations (payment gateways, Azure Cognitive Services, third-party REST APIs) belong in the Infrastructure layer, behind an interface declared in the Application layer, exactly like database access. You define an abstraction such as `IPaymentGateway` in `MyApp.Application`, and implement it in `MyApp.Infrastructure` using `HttpClient` (configured via `IHttpClientFactory` with Polly retry/circuit-breaker policies), keeping the Use Case unaware of HTTP details, base URLs, or the third party's DTOs. Response payloads from the external API are mapped into Application/Domain models inside the Infrastructure implementation, so a change to the vendor's contract never leaks into Use Cases. This is especially important on Azure, where you'd typically register the `HttpClient` with `AddHttpClient<IPaymentGateway, StripePaymentGateway>()` and store API keys in Azure Key Vault rather than appsettings. Isolating external calls this way also allows Use Cases to be unit tested by mocking `IPaymentGateway`, without making real network calls in the test suite. If the external call is asynchronous/event-driven (e.g. a webhook or Azure Service Bus message), the Infrastructure layer still owns the transport concern, translating the inbound message into a Domain Event or command handled by the Application layer.

```csharp
public interface IPaymentGateway
{
    Task<PaymentResult> ChargeAsync(decimal amount, string customerId, CancellationToken ct);
}

public class StripePaymentGateway : IPaymentGateway
{
    private readonly HttpClient _httpClient;
    public StripePaymentGateway(HttpClient httpClient) => _httpClient = httpClient;
    public async Task<PaymentResult> ChargeAsync(decimal amount, string customerId, CancellationToken ct)
    {
        var response = await _httpClient.PostAsJsonAsync("charges", new { amount, customerId }, ct);
        return await response.Content.ReadFromJsonAsync<PaymentResult>(cancellationToken: ct);
    }
}
```

---


## Explain the control flow of a user interacting with Clean Architecture components?
A user action first hits the Outer layer - an ASP.NET Core Controller or minimal API endpoint - which authenticates/authorizes the request (e.g. via JWT bearer tokens issued by Azure AD/Entra ID) and maps the HTTP payload into a Command/Query object. That object is dispatched, typically through MediatR, to a Use Case handler in the Application layer, which loads relevant Domain Entities via repository interfaces, invokes business methods on them to enforce invariants, and persists changes back through the same interfaces. The Infrastructure layer's concrete implementations (EF Core against MSSQL, Azure Service Bus publishers) execute the actual I/O without the Use Case knowing the technical details. Once the Use Case completes, it returns a result up the call stack to the Controller, which the Presenter/Controller then maps into an HTTP response (status code + JSON body) sent back to the user. If the operation raises Domain Events (e.g. `OrderPlacedEvent`), these are typically dispatched after the transaction commits, triggering side effects such as sending an email or publishing an integration event to Azure Service Bus for other microservices to consume. Throughout this flow, control always crosses layer boundaries through interfaces defined in the Application layer, keeping the flow's direction consistent with the Dependency Rule.

```csharp
// Simplified flow: Controller -> Mediator -> Handler -> Domain -> Repository -> DbContext
public async Task<IActionResult> Post([FromBody] CreateOrderRequest request) =>
    Ok(await _mediator.Send(new PlaceOrderCommand(request.CustomerId, request.Lines)));
```

---


## Compare Onion vs Clean vs Hexagonal Architectures
Onion Architecture (Jeffrey Palermo) was the first to formalize concentric layers with the Domain Model at the center, surrounded by Domain Services, then Application Services, with Infrastructure and UI as the outermost ring, with all dependencies pointing inward - the direct predecessor of Clean Architecture. Clean Architecture (Robert C. Martin) builds on the same idea but adds explicit named components - Entities, Use Cases, Interface Adapters (Controllers/Presenters/Gateways), and Frameworks & Drivers - making the boundaries and responsibilities more prescriptive. Hexagonal Architecture (Alistair Cockburn), also called Ports and Adapters, frames the same inversion differently: the application core exposes "Ports" (interfaces) and external systems connect through "Adapters" that implement or consume those ports, without necessarily prescribing internal layering like Use Cases vs Entities. In a .NET solution, all three manifest almost identically in practice - Domain/Application projects with no outward dependencies, and Infrastructure projects implementing interfaces to talk to MSSQL, Azure services, or external APIs - the differences are largely terminology and where you draw the boundary lines rather than fundamentally different rules. Hexagonal is the most flexible/least prescriptive about internal structure, Onion is the most focused on the Domain Model at the core, and Clean Architecture provides the most detailed component vocabulary (Entities, Use Cases, Interface Adapters). Choosing between them is mostly a matter of team convention, since the underlying goal - isolating business logic from frameworks and infrastructure via the Dependency Rule/Inversion of Control - is shared by all three.

```csharp
// Hexagonal terminology mapped to Clean Architecture equivalents
public interface IOrderPort { Task PlaceOrderAsync(Order order); } // "Port" == Application interface
public class SqlOrderAdapter : IOrderPort { /* "Adapter" == Infrastructure implementation */ }
```

---


## What is the difference between Request/Response Models and Entities in Clean Architecture?
Entities live in the Domain layer and represent core business objects with behavior and invariants, independent of any transport format - they should never be serialized directly to/from JSON in a Web API. Request/Response Models (often called DTOs, view models, or Application layer input/output models) live at the Application/Presentation boundary and represent exactly the shape of data a client sends or receives, including only the fields relevant to that specific operation. For example, a `CreateOrderRequest` might contain a flat list of product IDs and quantities, while the `Order` Entity contains richer invariants, computed totals, and possibly private setters that a JSON deserializer couldn't populate directly. Keeping them separate (with AutoMapper/Mapster handling translation) prevents over-posting/under-posting vulnerabilities, avoids exposing internal Domain structure or database identifiers unintentionally, and lets the API contract evolve independently of the Domain model's refactoring. It also allows different Use Cases to expose different slices of the same Entity - e.g. an `OrderSummaryResponse` for a list view versus a full `OrderDetailsResponse` for a detail view - without changing the Entity itself. This separation is a direct consequence of the Dependency Rule, since Presentation-layer concerns (serialization attributes, validation attributes like `[Required]`) must not contaminate the Domain layer.

```csharp
public record CreateOrderRequest(Guid CustomerId, List<OrderLineDto> Lines);
public record OrderResponse(Guid Id, string Status, decimal Total);
```

---


## How and where do you use transactions in the Clean Architecture?
Transaction management is an Infrastructure concern but is typically scoped at the Use Case boundary in the Application layer, so a whole business operation either fully commits or fully rolls back. A common .NET pattern is wrapping each MediatR handler with a `TransactionBehavior` pipeline (an `IPipelineBehavior<TRequest, TResponse>`) that begins a `DbContext` transaction (or relies on EF Core's `SaveChangesAsync` implicit transaction) before the handler runs and commits it after, rolling back automatically if an exception propagates. For operations spanning multiple aggregates or repositories against the same MSSQL database, an explicit `IDbContextTransaction` or `TransactionScope` ensures atomicity across multiple `SaveChanges` calls. When the operation must also publish integration events to Azure Service Bus, the Outbox pattern is preferred over a distributed transaction (2PC), persisting the event in the same MSSQL transaction as the business data and having a background dispatcher publish it afterward, guaranteeing at-least-once delivery without cross-service transactions. The Domain and Application layers should never contain raw ADO.NET/EF Core transaction code directly; instead, they depend on a `IUnitOfWork` abstraction that Infrastructure implements. This keeps transactional consistency an Infrastructure detail while the Use Case logic simply expresses "this must happen atomically."

```csharp
public class TransactionBehavior<TRequest, TResponse> : IPipelineBehavior<TRequest, TResponse>
{
    private readonly AppDbContext _db;
    public TransactionBehavior(AppDbContext db) => _db = db;

    public async Task<TResponse> Handle(TRequest request, RequestHandlerDelegate<TResponse> next, CancellationToken ct)
    {
        await using var transaction = await _db.Database.BeginTransactionAsync(ct);
        var response = await next();
        await transaction.CommitAsync(ct);
        return response;
    }
}
```

---
