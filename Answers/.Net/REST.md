# REST


## Contents
- [What is REST Web Services?](#what-is-rest-web-services)
- [Which protocol is used by RESTful webservices?](#which-protocol-is-used-by-restful-webservices)
- [What is RESTful Web Services?](#what-is-restful-web-services)
- [What REST stands for?](#what-rest-stands-for)
- [What is a Resource in Restful web services?](#what-is-a-resource-in-restful-web-services)
- [Mention what is the difference between AJAX and REST?](#mention-what-is-the-difference-between-ajax-and-rest)
- [What is purpose of a URI in REST based webservices?](#what-is-purpose-of-a-uri-in-rest-based-webservices)
- [What are different HTTP Methods supported in Restful Web Services?](#what-are-different-http-methods-supported-in-restful-web-services)
- [Mention some key characteristics of REST?](#mention-some-key-characteristics-of-rest)
- [Mention what are resources in a REST architecture?](#mention-what-are-resources-in-a-rest-architecture)
- [What are advantages of REST web services?](#what-are-advantages-of-rest-web-services)
- [What's the difference between REST & RESTful?](#whats-the-difference-between-rest--restful)
- [What is addressing in RESTful webservices?](#what-is-addressing-in-restful-webservices)
- [What is messaging in RESTful webservices?](#what-is-messaging-in-restful-webservices)
- [What is statelessness in RESTful Webservices?](#what-is-statelessness-in-restful-webservices)
- [What are disadvantages of REST web services?](#what-are-disadvantages-of-rest-web-services)
- [What are the disadvantages of statelessness in RESTful Webservices?](#what-are-the-disadvantages-of-statelessness-in-restful-webservices)
- [WebSockets vs Rest API for real time data? Which to choose?](#websockets-vs-rest-api-for-real-time-data-which-to-choose)
- [What should be the purpose of OPTIONS method of RESTful web services?](#what-should-be-the-purpose-of-options-method-of-restful-web-services)
- [What are the advantages of statelessness in RESTful Webservices?](#what-are-the-advantages-of-statelessness-in-restful-webservices)
- [What should be the purpose of HEAD method of RESTful web services?](#what-should-be-the-purpose-of-head-method-of-restful-web-services)
- [What is difference between OData and REST web services?](#what-is-difference-between-odata-and-rest-web-services)
- [Explain the difference between WCF, Web API, WCF REST and Web Service?](#explain-the-difference-between-wcf-web-api-wcf-rest-and-web-service)
- [Enlist some important constraints for RESTful web services](#enlist-some-important-constraints-for-restful-web-services)
- [What are the best practices to be followed while designing a secure RESTful web service?](#what-are-the-best-practices-to-be-followed-while-designing-a-secure-restful-web-service)
- [Name some best practices for better RESTful API design](#name-some-best-practices-for-better-restful-api-design)

---


## What is REST Web Services?
REST (Representational State Transfer) is an architectural style for designing networked applications, defined by Roy Fielding, that treats server-side data as resources which clients manipulate through a uniform, stateless interface, typically over HTTP. A REST web service exposes those resources as URIs (e.g., `/api/orders/5`) and lets clients perform operations on them using standard HTTP verbs (GET, POST, PUT, DELETE), with the resource's state represented in a portable format like JSON or XML. Unlike SOAP, REST is not a protocol or a strict standard but a set of architectural constraints (statelessness, uniform interface, cacheability, layered system, client-server separation) that, when followed, produce loosely coupled, scalable, and easily consumable services. In an ASP.NET Core Web API, REST is implemented via `[ApiController]`-decorated controllers where each action maps to an HTTP verb and route, and model binding/serialization handles converting between the wire format and C# objects automatically. REST web services are the dominant style for public and internal APIs today because of their simplicity, statelessness (enabling horizontal scaling), and natural fit with HTTP infrastructure like caching, load balancers, and CDNs. On Azure, REST APIs are commonly hosted on App Service or as Azure Functions HTTP triggers, and Azure API Management sits in front to handle throttling, versioning, and authentication centrally. Because REST relies on standard HTTP semantics, it integrates naturally with existing web tooling (browsers, `curl`, Postman, `HttpClient`) without requiring specialized clients or generated proxies.

```csharp
[ApiController]
[Route("api/orders")]
public class OrdersController : ControllerBase {
    [HttpGet("{id}")]
    public async Task<ActionResult<Order>> GetOrder(int id) {
        var order = await _orderService.GetByIdAsync(id);
        return order is null ? NotFound() : Ok(order);
    }
}
```

---


## Which protocol is used by RESTful webservices?
RESTful web services are built on top of HTTP (or HTTPS for secure transport), leveraging its existing verbs, status codes, and headers rather than defining a custom application-layer protocol. This is a key distinction from SOAP, which is protocol-agnostic in theory but almost always layered over HTTP with its own XML envelope and can technically run over other transports like SMTP. Because REST is tied to HTTP semantics, it directly reuses HTTP status codes (200, 201, 400, 404, 500), HTTP caching headers (`ETag`, `Cache-Control`), and content negotiation (`Accept`/`Content-Type` headers) instead of inventing its own equivalents. In ASP.NET Core, the entire Web API pipeline (Kestrel, routing, middleware) is built directly on HTTP, so REST controllers naturally inherit all of HTTP's transport-level features like keep-alive connections, compression, and TLS. HTTPS is mandatory for any production REST API handling sensitive data (credentials, PII, tokens) since plain HTTP exposes headers and payloads to interception; ASP.NET Core enforces this easily via `UseHttpsRedirection()` and HSTS middleware. On Azure, App Service and Azure Front Door/Application Gateway terminate TLS and can enforce HTTPS-only access at the platform level, adding another layer of protocol-level security. While REST is most associated with HTTP/1.1, modern REST APIs increasingly run over HTTP/2 or HTTP/3 for improved multiplexing and performance without any change to the REST architectural style itself.

```csharp
builder.Services.AddHsts(options => options.MaxAge = TimeSpan.FromDays(365));

var app = builder.Build();
app.UseHttpsRedirection(); // enforces HTTP -> HTTPS on every request
app.UseHsts();
```

---


## What is RESTful Web Services?
"RESTful" describes a web service that actually adheres to REST's architectural constraints, as opposed to merely using HTTP as a transport while ignoring REST principles (sometimes derisively called a "REST-like" or RPC-over-HTTP API). A truly RESTful service treats every piece of data as an addressable resource with its own URI, uses HTTP verbs semantically correct (GET for reads, POST for creation, PUT/PATCH for updates, DELETE for removal), remains fully stateless between requests, and ideally supports HATEOAS (Hypermedia as the Engine of Application State) so responses include links guiding clients to related actions. In practice, many APIs labeled "REST APIs" are only loosely RESTful — for example, using POST for everything or embedding actions in the URL like `/api/getOrderById` instead of `/api/orders/{id}` — which technically violates the uniform interface constraint but is still commonly accepted in industry as "RESTful enough." In ASP.NET Core, achieving genuine RESTfulness means designing routes around nouns (resources) rather than verbs, using appropriate status codes (201 Created with a `Location` header for POST, 204 No Content for successful DELETE), and avoiding server-side session state so any instance can handle any request — critical for horizontal scaling on Azure App Service or behind a load balancer. Richardson's Maturity Model is a common framework for grading how RESTful an API truly is, from Level 0 (single URI, single verb — essentially RPC) up to Level 3 (full HATEOAS). Most production APIs target Level 2 (proper resources and HTTP verbs/status codes) since full HATEOAS is often seen as adding complexity without proportional benefit for typical client needs.

```csharp
// Level 3 (HATEOAS): response includes links to related actions
public record OrderResponse(int Id, decimal Total, List<LinkDto> Links);

var response = new OrderResponse(order.Id, order.Total, new List<LinkDto> {
    new("self", $"/api/orders/{order.Id}", "GET"),
    new("cancel", $"/api/orders/{order.Id}/cancel", "POST")
});
```

---


## What REST stands for?
REST stands for **Re**presentational **S**tate **T**ransfer, a term coined by Roy Fielding in his 2000 doctoral dissertation, which describes an architectural style rather than a specific technology or protocol. "Representational" refers to the idea that clients interact with a *representation* of a resource's state (e.g., a JSON document) rather than the resource itself, which lives on the server (e.g., a row in a SQL Server table); the same underlying resource can have multiple representations (JSON, XML, HTML) depending on what the client requests via content negotiation. "State Transfer" refers to how each request from the client to the server must contain all the information needed to understand and process it — the server transfers the resource's current representation to the client, and the client can transfer a new desired state back (e.g., via PUT/PATCH), without the server retaining any session-specific context between requests. This naming reflects REST's core statelessness constraint: unlike stateful protocols where the server remembers a client's session, REST interactions are self-contained, making each request/response an independent transfer of state representation. Understanding the etymology helps clarify why REST APIs shouldn't rely on server-side session variables to track a client across multiple calls — every request should be able to stand alone, authenticated via a bearer token or API key rather than a server-tracked session ID. This design principle is why REST APIs scale so well horizontally: any server instance behind a load balancer can handle any request without needing "sticky sessions," which is especially valuable in Azure App Service's auto-scaling and multi-instance deployment scenarios.

```csharp
// State transfer: client sends the full desired representation, server transfers back the current one
[HttpPut("{id}")]
public async Task<ActionResult<Order>> UpdateOrder(int id, OrderDto dto) {
    var updated = await _service.ReplaceAsync(id, dto);
    return Ok(updated); // representation of the new state is transferred back
}
```

---


## What is a Resource in Restful web services?
A resource is any piece of information or entity that can be named, addressed, and manipulated through the API — a customer, an order, a product, or even a collection of these (e.g., "all orders for customer 5") — and each resource is uniquely identified by a URI. In an ASP.NET Core Web API backed by SQL Server, a resource typically maps to a row (or a computed/aggregate view) in the database, exposed through routes like `/api/customers/42` for a single customer or `/api/customers/42/orders` for that customer's orders as a sub-resource collection. Resources are conceptually distinct from their representations: the resource "Order #123" is an abstract concept living in your database, while the representation returned to the client (JSON with specific fields) is just one possible view of that resource's current state, and different clients could request different representations (JSON vs. XML) of the exact same resource. Designing good resource models means thinking in terms of nouns, not actions — instead of an endpoint like `/api/calculateOrderTotal`, you'd expose `/api/orders/{id}/total` as a sub-resource, or compute the total as a field on the order resource itself. Resource identifiers should be stable and not change over the resource's lifetime, since clients, bookmarks, and caches depend on that stability — using a database's immutable primary key (rather than something mutable like an email address) as the URI identifier is the standard practice. Collections and single-item resources are usually pluralized consistently (`/api/orders` for the collection, `/api/orders/{id}` for a single item) to keep the API intuitive and predictable for consumers.

```csharp
[HttpGet("{customerId}/orders")] // sub-resource collection under a parent resource
public async Task<ActionResult<List<Order>>> GetCustomerOrders(int customerId) {
    var orders = await _context.Orders
        .Where(o => o.CustomerId == customerId)
        .ToListAsync();
    return Ok(orders);
}
```

---


## Mention what is the difference between AJAX and REST?
AJAX (Asynchronous JavaScript and XML) is a browser-side technique for making asynchronous HTTP requests from client-side JavaScript without reloading the page, while REST is a server-side architectural style for designing the API that AJAX calls might be talking to — they operate at completely different layers and aren't directly comparable, but are often mentioned together because AJAX is a very common way to consume a REST API from a web frontend. AJAX doesn't care what kind of backend it's calling — it can hit a RESTful API, a SOAP endpoint, a GraphQL endpoint, or a plain non-RESTful script; it's purely a transport/client mechanism (traditionally using `XMLHttpRequest`, now more commonly the `fetch` API) for sending and receiving data asynchronously. REST, on the other hand, defines constraints on how the server exposes and organizes its resources (statelessness, uniform interface, resource-based URIs), completely independent of how a client chooses to call it. A concrete example: a React or Angular frontend uses AJAX-style `fetch`/`HttpClient` calls to hit an ASP.NET Core Web API's RESTful endpoints (`GET /api/orders`), receiving JSON back and updating the DOM without a full page reload. The key point for an interview is recognizing this isn't really an "either/or" comparison — AJAX is a client-side networking technique, REST is a server-side API design philosophy, and they commonly work together but solve entirely different problems. Modern SPA frameworks rarely say "AJAX" explicitly anymore (they use `fetch`, `axios`, or Angular's `HttpClient`), but the underlying concept — asynchronous XHR-style calls to a backend API — remains the same.

```javascript
// AJAX-style call (fetch) consuming a RESTful ASP.NET Core endpoint
const response = await fetch("/api/orders/5");
const order = await response.json();
```

---


## What is purpose of a URI in REST based webservices?
A URI (Uniform Resource Identifier) in a RESTful service serves as the unique, stable address for a specific resource or resource collection, forming the foundation of REST's "addressability" constraint — every piece of data you can interact with must have its own identifiable location. Well-designed URIs are hierarchical and noun-based, reflecting the resource's place in the domain model, e.g., `/api/customers/42/orders/7` clearly indicates "order 7 belonging to customer 42," making the API self-descriptive and predictable without needing to consult documentation for every endpoint. URIs should remain stable over time — even if the underlying implementation changes, the same URI should keep pointing to the same conceptual resource, since clients, bookmarks, caches, and hyperlinks (in HATEOAS-style APIs) depend on that permanence. In ASP.NET Core, URIs are defined through attribute routing (`[Route("api/customers/{customerId}/orders/{orderId}")]`), which binds route segments directly to action parameters, keeping the mapping between URI structure and controller logic explicit and easy to maintain. Good URI design avoids verbs (`/api/getCustomerOrders`) in favor of nouns and standard HTTP verbs to express the action (`GET /api/customers/42/orders`), and uses query parameters for filtering/sorting/pagination rather than encoding them into the path itself (e.g., `/api/orders?status=pending&page=2`). On the infrastructure side, stable, well-structured URIs also make caching (via CDNs, reverse proxies, or Azure Front Door) and API Management policies (rate limiting per resource path) much easier to configure correctly.

```csharp
[Route("api/customers/{customerId}/orders/{orderId}")]
[HttpGet]
public async Task<ActionResult<Order>> GetOrder(int customerId, int orderId) {
    var order = await _service.GetAsync(customerId, orderId);
    return order is null ? NotFound() : Ok(order);
}
```

---


## What are different HTTP Methods supported in Restful Web Services?
REST APIs use standard HTTP methods, each with well-defined semantics: `GET` retrieves a resource or collection without side effects (safe and idempotent), `POST` creates a new resource or triggers a non-idempotent server-side action (not idempotent — calling it twice can create two records), `PUT` replaces a resource entirely with the provided representation (idempotent — calling it repeatedly with the same body produces the same result), `PATCH` applies a partial update to a resource (not guaranteed idempotent, depends on implementation), and `DELETE` removes a resource (idempotent — deleting an already-deleted resource is still "deleted"). Less commonly used but still important are `HEAD` (like GET but returns only headers, no body — useful for checking existence or metadata cheaply) and `OPTIONS` (used to discover which methods/headers a resource supports, and critical for CORS preflight requests in browsers). In ASP.NET Core, each verb maps to an attribute on a controller action (`[HttpGet]`, `[HttpPost]`, `[HttpPut]`, `[HttpPatch]`, `[HttpDelete]`), and the framework automatically routes incoming requests to the matching action based on both the verb and the route template. Correctly choosing idempotent vs. non-idempotent verbs matters for reliability: clients (and Polly-based retry policies) can safely retry a `PUT`/`DELETE` on a transient failure without side effects, but retrying a `POST` blindly can create duplicate resources unless paired with an idempotency key. Following HTTP semantics correctly also lets intermediate infrastructure (browsers, proxies, CDNs, Azure API Management) make correct assumptions — for example, caching only `GET` responses by default, since caching a `POST` result would be semantically wrong. Misusing verbs (e.g., using `GET` to delete a record via a query string) breaks these assumptions and can cause serious bugs, such as a web crawler or browser prefetcher accidentally triggering destructive side effects.

```csharp
[HttpGet("{id}")]
public async Task<ActionResult<Order>> Get(int id) => Ok(await _service.GetAsync(id));

[HttpPost]
public async Task<ActionResult<Order>> Create(OrderDto dto) {
    var created = await _service.CreateAsync(dto);
    return CreatedAtAction(nameof(Get), new { id = created.Id }, created);
}

[HttpPut("{id}")]
public async Task<IActionResult> Replace(int id, OrderDto dto) {
    await _service.ReplaceAsync(id, dto);
    return NoContent();
}

[HttpDelete("{id}")]
public async Task<IActionResult> Delete(int id) {
    await _service.DeleteAsync(id);
    return NoContent();
}
```

---


## Mention some key characteristics of REST?
REST is defined by a set of architectural constraints: a **client-server** separation, where the UI/client and the data storage/business logic evolve independently; **statelessness**, meaning each request must contain all information needed to process it, with no session state stored on the server between requests; a **uniform interface**, standardizing how resources are identified (URIs), manipulated (HTTP verbs), self-described (media types like JSON), and linked (HATEOAS); **cacheability**, where responses explicitly indicate whether they can be cached (via `Cache-Control`/`ETag` headers) to improve performance and scalability; a **layered system**, allowing intermediaries like load balancers, API gateways, or CDNs to sit between client and server transparently; and optionally **code-on-demand**, where the server can extend client functionality by sending executable code (rarely used in practice, e.g., JavaScript sent to a browser). In an ASP.NET Core Web API, statelessness is achieved by avoiding server-side session objects and instead relying on tokens (JWT) sent with every request; the layered system constraint is realized in Azure by placing Azure API Management or Application Gateway in front of the actual App Service. Cacheability is implemented via response headers (`[ResponseCache]` attribute in ASP.NET Core) or `ETag`-based conditional GETs, letting clients avoid re-fetching unchanged data. These constraints work together to produce APIs that scale horizontally (any server can handle any request since there's no session affinity), are simpler to reason about (uniform interface means less bespoke logic per endpoint), and are resilient to intermediary failures (layered system allows retries/caching at any tier). Violating these constraints — e.g., storing session state in memory on a specific server instance — quickly breaks horizontal scalability and load-balancer compatibility, which is a common real-world REST design mistake.

```csharp
[HttpGet("{id}")]
[ResponseCache(Duration = 60)] // cacheability constraint via standard HTTP headers
public async Task<ActionResult<Order>> GetOrder(int id) => Ok(await _service.GetAsync(id));
```

---


## Mention what are resources in a REST architecture?
In REST, resources are the fundamental building blocks of the API's information model — anything a client might want to reference, retrieve, or manipulate, exposed as identifiable, addressable entities via URIs. Resources can be singular (a specific customer, `/api/customers/42`) or collections (all customers, `/api/customers`), and can also be more abstract concepts like a computed report, a search result set, or a process/workflow state (e.g., `/api/orders/7/status`). What makes something a "resource" in REST terms is that it has a distinct identity and state that can be represented and transferred to a client — it doesn't need to correspond one-to-one with a database table; it could be an aggregate composed of data from multiple tables (e.g., an "Order Summary" resource joining Orders, Customers, and LineItems). Resource design should reflect how consumers naturally think about the domain rather than mirroring the database schema directly — for instance, exposing `/api/orders/{id}/invoice` as a resource even if "invoice" is computed on the fly rather than stored as its own table. Sub-resources (nested under a parent, like `/api/customers/42/addresses`) express ownership/containment relationships, which is a natural way to model one-to-many relationships in the URI hierarchy without over-nesting (generally 2-3 levels deep is a good practical limit before it becomes unwieldy). Properly modeling resources — rather than modeling remote procedure calls — is what separates a genuinely RESTful API from an RPC-style API merely running over HTTP, and it directly impacts how intuitive, cacheable, and maintainable the API is over its lifetime.

```csharp
// Computed/aggregate resource, not a 1:1 database table
[HttpGet("{id}/invoice")]
public async Task<ActionResult<InvoiceDto>> GetInvoice(int id) {
    var invoice = await _invoiceService.BuildFromOrderAsync(id);
    return Ok(invoice);
}
```

---


## What are advantages of REST web services?
REST's biggest advantage is simplicity — it reuses existing, well-understood HTTP infrastructure (verbs, status codes, headers) rather than requiring a custom protocol, generated client stubs, or heavyweight tooling, making it easy to consume from virtually any language or platform, including `curl` and browsers directly. Statelessness enables straightforward horizontal scalability: because no server instance needs to remember client session state, requests can be load-balanced across any number of identical instances (e.g., Azure App Service scaling out under load) without sticky sessions or shared session storage. REST's reliance on standard HTTP caching semantics (`ETag`, `Cache-Control`, CDN-friendly `GET` requests) means performance optimizations come almost for free, unlike more custom protocols where caching has to be built manually. The lightweight JSON payloads typical of REST APIs are smaller and faster to parse than the verbose XML envelopes SOAP requires, reducing bandwidth and improving client-side performance, especially on mobile networks. REST's uniform interface (predictable URI/verb conventions) reduces the learning curve for new consumers of the API and makes auto-generated documentation (via Swagger/OpenAPI/Swashbuckle in ASP.NET Core) straightforward and accurate. Because REST APIs are just HTTP endpoints, they integrate naturally with the broader web ecosystem — API gateways, reverse proxies, browser dev tools, and monitoring tools (like Application Insights) all understand HTTP natively without special adapters. Finally, REST's flexibility around content negotiation lets the same endpoint serve JSON to modern clients and XML to legacy consumers if truly needed, without maintaining two separate services.

```csharp
// Content negotiation: same endpoint, format chosen via the Accept header
builder.Services.AddControllers()
    .AddXmlSerializerFormatters(); // adds XML alongside the default JSON formatter
```

---


## What's the difference between REST & RESTful?
"REST" refers to the architectural style itself — the set of constraints (statelessness, uniform interface, cacheability, layered system, client-server separation) defined by Roy Fielding — while "RESTful" is the adjective describing an actual API or service that adheres to those constraints. In practice, the terms are often used almost interchangeably in casual conversation ("a REST API" and "a RESTful API" usually mean the same thing), but strictly speaking, REST is the theory/style, and RESTful is the practical implementation that conforms to it. This distinction matters because many APIs marketed as "REST APIs" don't actually follow all REST constraints strictly — for example, an API that uses only `POST` for every operation, embeds actions in URLs (`/api/deleteOrder?id=5` instead of `DELETE /api/orders/5`), or maintains server-side session state technically isn't fully "RESTful" even though it's HTTP-based and JSON-returning. An API that genuinely follows the constraints — resource-oriented URIs, correct HTTP verb usage, statelessness, appropriate status codes, and ideally HATEOAS — earns the "RESTful" label more accurately. In an interview context, being able to articulate this nuance (REST = the architectural style/theory, RESTful = an implementation that actually conforms to it) shows a deeper understanding than just treating them as synonyms. Most production APIs, including typical ASP.NET Core Web APIs, are "RESTful" in the pragmatic sense (proper verbs, resource-based routes, statelessness) without going all the way to full HATEOAS, which is generally accepted as good enough for real-world RESTful design (Richardson Maturity Model Level 2).

```csharp
// REST in name only: verb embedded in the URL, always POST
[HttpPost("deleteOrder")]
public IActionResult DeleteOrderBad([FromQuery] int id) => Ok();

// Genuinely RESTful: noun-based resource, correct HTTP verb
[HttpDelete("{id}")]
public IActionResult DeleteOrder(int id) => NoContent();
```

---


## What is addressing in RESTful webservices?
Addressing refers to REST's requirement that every resource be uniquely identifiable and reachable via its own URI, forming the basis of how clients locate and interact with data in a RESTful system. Rather than a single endpoint handling multiple resource types via parameters (as in RPC-style APIs), REST addressing means each distinct piece of data — a customer, an order, a specific line item — has its own dedicated address, e.g., `/api/customers/42`, `/api/orders/7`, `/api/orders/7/items/3`. This addressability is what enables REST's uniform interface: because every resource has a stable, predictable address, clients can construct URIs programmatically, bookmark them, cache responses against them, and follow hyperlinks (in HATEOAS-enabled APIs) without needing out-of-band knowledge of the API's internal structure. In ASP.NET Core, addressing is implemented through attribute routing, where route templates like `[Route("api/customers/{customerId}/orders/{orderId}")]` directly express this addressable hierarchy, and the `Location` header returned from a successful `POST` (via `CreatedAtAction`) tells the client the exact address of the newly created resource. Good addressing design keeps URIs meaningful and hierarchical (reflecting parent-child resource relationships) while avoiding excessive nesting that makes URIs unwieldy or brittle to schema changes. Since URIs act as a contract with API consumers, changing them without a versioning strategy is a breaking change — so URI stability is treated as seriously as any other part of the public API surface. Proper addressing also plays well with HTTP infrastructure: proxies, CDNs, and Azure API Management can apply per-resource-path rules (caching, rate limiting, authorization policies) precisely because each resource has a distinct, addressable path.

```csharp
[HttpPost]
public async Task<ActionResult<Order>> Create(OrderDto dto) {
    var created = await _service.CreateAsync(dto);
    // Location header gives the client the exact address of the new resource
    return CreatedAtAction(nameof(GetOrder), new { id = created.Id }, created);
}
```

---


## What is messaging in RESTful webservices?
Messaging in REST refers to how clients and servers exchange information — each interaction is a self-contained HTTP request/response message pair, where the request specifies the desired action (via method + URI + headers + optional body) and the response returns a status code, headers, and an optional body representing the resource's state. Because REST is stateless, every message must be independently interpretable — the server cannot rely on any prior message to understand the current one, so authentication tokens, content type, and any other context must be included in each request (e.g., an `Authorization: Bearer <jwt>` header on every call). The message body's format is negotiated via the `Content-Type` (what the client is sending) and `Accept` (what the client wants back) headers, most commonly JSON in modern APIs, though XML or other media types are also possible under REST's uniform interface constraint. In ASP.NET Core, the framework's model binding and serialization pipeline (`System.Text.Json` by default) automatically handles converting incoming JSON message bodies into C# objects and serializing outgoing objects back to JSON, based on these content negotiation headers. Proper REST messaging also relies on meaningful HTTP status codes as part of the "message" — a `201 Created` with a `Location` header, a `400 Bad Request` with a structured error body (e.g., RFC 7807 Problem Details), or a `404 Not Found` all communicate outcome without requiring the client to parse the response body to understand success/failure. Because each message is self-contained and stateless, REST messaging naturally supports retries, load balancing across multiple server instances, and asynchronous processing patterns (e.g., returning `202 Accepted` with a polling URL for long-running operations) without any special session-tracking infrastructure.

```csharp
[HttpPost("reports")]
public IActionResult StartReport(ReportRequest request) {
    var jobId = _reportQueue.Enqueue(request);
    return Accepted($"/api/reports/{jobId}"); // 202 + polling URL
}
```

---


## What is statelessness in RESTful Webservices?
Statelessness means the server does not store any client-specific session context between requests — every request must carry all the information the server needs to fully understand and process it, typically via headers (an auth token), query parameters, or the request body, rather than relying on server-remembered state from a previous call. This is fundamentally different from traditional stateful web applications (like classic ASP.NET Web Forms with `Session` state) where the server maintains an in-memory session tied to a specific client across multiple requests, usually via a session cookie routed back to the same server instance. In an ASP.NET Core Web API, statelessness is achieved by using stateless authentication (JWT bearer tokens validated on every request) instead of server-side sessions, and by never storing per-user data in static fields, `IMemoryCache` tied to a specific user, or other server-local state that wouldn't be visible to a different instance handling the next request. The huge practical benefit is horizontal scalability: because any server instance can handle any request without needing to "remember" the client, you can freely add or remove instances behind a load balancer (Azure App Service auto-scale) without sticky sessions, and a server crash or restart doesn't lose any in-flight session data since there isn't any to lose. Statelessness does shift more responsibility to the client, which must resend authentication credentials and any needed context with every call, and it can increase payload size slightly compared to relying on a cheap session ID — but this tradeoff is almost always worth it for scalability and resilience. It's worth distinguishing "stateless service" from "stateless data" — the application itself remains stateless even though the underlying database (SQL Server) obviously retains persistent state; statelessness specifically refers to not tying a client's session to a specific server instance's in-memory state.

```csharp
[HttpGet("me")]
[Authorize]
public IActionResult GetCurrentUser() {
    // identity comes from the bearer token on this request, not server-side session
    var userId = User.FindFirstValue(ClaimTypes.NameIdentifier);
    return Ok(new { userId });
}
```

---


## What are disadvantages of REST web services?
REST's flexibility comes at the cost of a lack of strict, enforced contracts — unlike SOAP's WSDL, which formally defines every operation, REST relies on documentation (often OpenAPI/Swagger) that isn't always kept perfectly in sync with the actual implementation, so clients can more easily break if the API changes without a proper versioning strategy. Statelessness, while great for scalability, means every request must carry all necessary context (authentication tokens, filters, etc.), which can increase payload size and requires clients to resend information the server could otherwise "remember" in a stateful model. REST doesn't have a universally agreed-upon standard for more advanced features like transactions spanning multiple resources, complex querying (filtering/sorting across nested resources), or built-in support for partial responses — these are often solved with ad hoc conventions (query parameters, OData-style filters) rather than a formal spec everyone follows identically. Over-fetching and under-fetching are common REST pain points: a client might get more data than it needs from a resource endpoint (over-fetching) or need to make multiple round-trips to assemble a complete view (under-fetching), which is part of what motivated alternatives like GraphQL. REST also lacks native support for real-time, bidirectional communication — a REST API can't push updates to clients on its own, requiring polling, long-polling, or a separate protocol like WebSockets/SignalR alongside the REST API for live data. Versioning a REST API cleanly (URI versioning, header versioning, etc.) is a design challenge without a single "correct" universal answer, and poor versioning strategy is a common source of breaking changes for consumers. Finally, because REST's constraints are guidelines rather than enforced rules, it's easy for teams to build APIs that are "REST in name only," leading to inconsistent conventions across different endpoints or teams within the same organization.

```csharp
// Over-fetching: client only needs Id/Total but gets the entire entity graph
[HttpGet("{id}")]
public async Task<ActionResult<Order>> GetOrder(int id) =>
    Ok(await _context.Orders.Include(o => o.Items).Include(o => o.Customer).FirstAsync(o => o.Id == id));
```

---


## What are the disadvantages of statelessness in RESTful Webservices?
The main downside of statelessness is that every request must carry its own complete context, which increases the size of each individual request (repeating an auth token, tenant ID, or other contextual data on every call) compared to a stateful model where the server could remember this after an initial handshake. This can also push more computational work to the server per-request — for example, validating a JWT's signature and claims on every single call, rather than a cheap session-ID lookup, adds a small but real amount of CPU overhead multiplied across every request in a high-traffic API. Statelessness makes certain multi-step workflows more awkward to model: a wizard-style process that spans multiple HTTP requests (e.g., a multi-page checkout) can't rely on server-side "current step" state and must instead pass all relevant state back and forth via the request/response bodies or a database-backed record the client references by ID. It also shifts the burden of managing any needed "session-like" behavior (e.g., a shopping cart) onto explicit, addressable resources backed by persistent storage (a `Cart` table in SQL Server keyed by a cart ID) rather than convenient in-memory session objects, which requires more deliberate design work up front. Additionally, statelessness can make debugging harder in some cases, since there's no persistent server-side "conversation" to inspect — each request must be understood in isolation, requiring good correlation IDs and distributed tracing (e.g., Application Insights) to reconstruct a user's overall journey across multiple stateless calls. Despite these tradeoffs, they're almost universally accepted in modern API design because the scalability, resilience, and simplicity benefits of statelessness far outweigh the added per-request overhead and design effort.

```csharp
// Cart state modeled as an explicit, addressable resource instead of server-side session
[HttpPost("carts/{cartId}/items")]
public async Task<IActionResult> AddItem(Guid cartId, CartItemDto item) {
    await _cartService.AddItemAsync(cartId, item);
    return NoContent();
}
```

---


## WebSockets vs Rest API for real time data? Which to choose?
REST APIs are fundamentally request-response: the client must initiate every interaction, so "real-time" updates require the client to poll repeatedly (or use long-polling), which adds latency, wastes bandwidth on unchanged data, and increases server load proportional to polling frequency. WebSockets establish a single persistent, full-duplex connection between client and server, allowing the server to push data to the client the instant something changes, without the client needing to ask — making WebSockets (or SignalR, .NET's abstraction over WebSockets/long-polling/Server-Sent Events) the right choice for genuinely real-time scenarios like live chat, stock tickers, collaborative editing, or live dashboards. REST is the better choice for typical CRUD operations, resource-oriented interactions, and anything where request-response semantics naturally fit — it's simpler to build, test, cache, and secure, and it benefits from all the standard HTTP tooling (caching, load balancers, API gateways) that WebSockets largely bypass. A common and practical pattern is to use both together: REST for standard data operations (fetching historical data, submitting forms, CRUD) and WebSockets/SignalR specifically for the subset of features that truly need live push updates, rather than forcing an entire API to be one or the other. In ASP.NET Core, SignalR provides hubs that abstract away the underlying transport (falling back to long-polling if WebSockets aren't available) and integrates with Azure SignalR Service for scaling out real-time connections across multiple server instances without managing sticky connections yourself. Choosing REST purely for real-time data via aggressive polling is generally an anti-pattern once update frequency requirements get demanding, since it wastes resources and adds unnecessary latency compared to a push-based model. The decision ultimately comes down to whether the client needs to be told about changes proactively (WebSockets) or is fine asking for the current state on its own schedule (REST).

```csharp
public class NotificationsHub : Hub {
    public async Task NotifyOrderShipped(int orderId) {
        // pushes to connected clients instantly, no polling required
        await Clients.All.SendAsync("OrderShipped", orderId);
    }
}
```

---


## What should be the purpose of OPTIONS method of RESTful web services?
The `OPTIONS` HTTP method is used to discover the communication capabilities of a resource — specifically, which HTTP methods and headers are supported at a given endpoint — without actually performing any operation on the resource, making it a safe, side-effect-free "capability check." Its most practical, everyday use in modern web development is as the CORS "preflight" request: when a browser-based frontend makes a cross-origin request with a non-simple method (like `PUT`/`DELETE`) or custom headers, the browser automatically sends an `OPTIONS` request first to ask the server "are you willing to accept this actual request from this origin, with these headers/methods?" before sending the real request. In ASP.NET Core, the CORS middleware (`app.UseCors()`) automatically handles `OPTIONS` preflight requests and responds with the appropriate `Access-Control-Allow-*` headers based on the configured CORS policy, without requiring any explicit `[HttpOptions]` action in most cases. Beyond CORS, `OPTIONS` can also be used by API clients or tooling to introspect an endpoint's supported verbs programmatically (the response typically includes an `Allow` header listing supported methods, e.g., `Allow: GET, POST, PUT, DELETE`), which can help build generic API explorers or validate that a client isn't calling an unsupported method before attempting it. `OPTIONS` requests should never have side effects and should always be safe to call repeatedly without changing server state, consistent with REST's expectation that discovery/metadata operations remain read-only. Understanding `OPTIONS` is particularly important for troubleshooting CORS issues in production — a common real-world bug is a misconfigured CORS policy causing the preflight `OPTIONS` request to fail or be blocked, which then causes the browser to reject the actual request even though the server would have handled it correctly.

```csharp
builder.Services.AddCors(options => options.AddPolicy("Default", policy =>
    policy.WithOrigins("https://myapp.com")
          .WithMethods("GET", "POST", "PUT", "DELETE")
          .WithHeaders("Authorization", "Content-Type")));

app.UseCors("Default"); // handles OPTIONS preflight automatically
```

---


## What are the advantages of statelessness in RESTful Webservices?
The primary advantage of statelessness is horizontal scalability: since no server instance needs to remember a specific client's session, requests can be freely load-balanced across any number of identical server instances without sticky sessions, making it trivial to scale out (e.g., Azure App Service auto-scale rules) or scale back down without losing any client context. It also greatly improves resilience — if a server instance crashes or restarts, no in-flight session data is lost because there wasn't any server-side session state to begin with; the client simply retries against another available instance seamlessly. Statelessness simplifies the mental model for both API developers and consumers, since every request can be reasoned about in complete isolation without needing to track a conversation's history or worry about "what state is the server currently in for this client" — this also makes REST APIs significantly easier to test, since each test case is self-contained and doesn't depend on prior test execution order. It enables straightforward caching, since a stateless request's response depends only on the request itself (same URI + same headers = same expected response), which is exactly what HTTP caching semantics (`ETag`, `Cache-Control`) rely on — caching a stateful response correctly would be far more complex since it would depend on hidden server-side context. Deployment and operations also become simpler: rolling deployments, blue-green deployments, and zero-downtime updates are much easier when there's no server-affinity requirement, since any new instance can immediately start serving traffic without needing to "warm up" or migrate session state from old instances. Finally, statelessness reduces server memory pressure at scale, since the server isn't accumulating potentially large numbers of per-client session objects in memory — everything needed is passed in with each request and discarded afterward.

```csharp
// Same request, same expected response - safe to cache regardless of which instance handles it
[HttpGet("{id}")]
[ResponseCache(Duration = 30, VaryByHeader = "Authorization")]
public async Task<ActionResult<Order>> GetOrder(int id) => Ok(await _service.GetAsync(id));
```

---


## What should be the purpose of HEAD method of RESTful web services?
The `HEAD` method behaves exactly like `GET` but instructs the server to return only the response headers, omitting the response body entirely — it's used when a client wants metadata about a resource (its size via `Content-Length`, its last-modified date, whether it exists at all) without incurring the cost of transferring the full payload. A common practical use is checking whether a large resource (e.g., a file, an image, or a big JSON document) has changed since it was last cached, by comparing `ETag`/`Last-Modified` headers from a `HEAD` request against a locally cached copy, avoiding a full re-download unless necessary. It's also useful for cheaply verifying a resource's existence — a client can send `HEAD /api/orders/123` to check if order 123 exists (200 vs. 404) without pulling down the entire order payload, which is more efficient than a full `GET` when only existence matters. In ASP.NET Core, `HEAD` requests are automatically supported for any endpoint that supports `GET` — the framework runs the same action method but strips the response body before sending it back to the client, so developers typically don't need to write separate `[HttpHead]` handlers unless custom behavior is required. Because `HEAD` is safe and idempotent (just like `GET`), it's appropriate for automated health checks, monitoring tools, and crawlers that want to verify availability or freshness without generating unnecessary bandwidth or server-side processing costs. Supporting `HEAD` correctly (i.e., ensuring it returns the exact same headers `GET` would, just without the body) is part of building a properly RESTful, well-behaved API that plays nicely with caching proxies, monitoring tools, and HTTP-aware infrastructure like CDNs and API gateways.

```csharp
[HttpHead("{id}")] // ASP.NET Core reuses the GET action, strips the body automatically
[HttpGet("{id}")]
public async Task<ActionResult<Order>> GetOrder(int id) {
    var order = await _service.GetAsync(id);
    return order is null ? NotFound() : Ok(order);
}
```

---


## What is difference between OData and REST web services?
REST is a broad architectural style with no built-in, standardized query language — filtering, sorting, and pagination conventions are left entirely up to each API's own design (e.g., `?status=pending&page=2`), meaning every REST API can implement these differently. OData (Open Data Protocol) is a more prescriptive, standardized protocol built *on top of* REST principles that defines a formal, consistent query syntax for filtering, sorting, expanding related entities, and selecting specific fields directly via URI query parameters (e.g., `/api/orders?$filter=Status eq 'Pending'&$orderby=CreatedDate desc&$select=Id,Total`), all governed by a published specification rather than ad hoc conventions. In ASP.NET Core, OData is implemented via the `Microsoft.AspNetCore.OData` package, which adds these standardized query capabilities on top of your existing Web API controllers/EF Core models, translating OData query expressions directly into LINQ/SQL queries against the underlying data source. The advantage of OData is consistency and reduced client-side/server-side boilerplate — clients get a rich, self-describing querying capability (including a `$metadata` endpoint describing the entire data model) without every endpoint needing custom filter/sort logic hand-written for each resource. The tradeoff is added complexity and a tighter coupling between the API's query capabilities and its underlying data model, which can expose more of the internal schema than a hand-curated plain REST API might choose to, and can make it harder to optimize specific query patterns since OData translates fairly directly to the data layer. Plain REST is generally preferred for smaller or highly curated APIs where you want full control over exactly what queries are allowed, while OData shines for large, data-centric APIs (like enterprise reporting or admin backends) where rich, flexible querying is a core requirement and the standardized protocol saves significant development time.

```csharp
[HttpGet]
[EnableQuery] // enables $filter, $orderby, $select, $expand automatically
public IQueryable<Order> Get() => _context.Orders;

// GET /api/orders?$filter=Status eq 'Pending'&$orderby=CreatedDate desc
```

---


## Explain the difference between WCF, Web API, WCF REST and Web Service?
A classic ASMX "Web Service" is Microsoft's oldest SOAP-based web service technology (largely legacy/deprecated today), supporting only HTTP transport and XML/SOAP messaging, with no built-in support for REST-style resource-oriented design. WCF (Windows Communication Foundation) is a much more general-purpose, configurable framework for building service-oriented applications that can communicate over multiple protocols (HTTP, TCP, named pipes, MSMQ) and multiple message formats (SOAP, and to a lesser extent REST/JSON), making it far more flexible than ASMX but also considerably more complex to configure (bindings, contracts, behaviors). "WCF REST" refers to configuring WCF specifically to expose RESTful, HTTP+JSON endpoints instead of its default SOAP behavior, using `WebGet`/`WebInvoke` attributes and a `webHttpBinding` — this was Microsoft's early attempt at REST support before ASP.NET Web API existed, but it always felt somewhat bolted-on since WCF's core design centers around SOAP-style service contracts. ASP.NET Web API (and its modern successor, ASP.NET Core Web API) was purpose-built from the ground up specifically for HTTP and REST, with first-class support for content negotiation, HTTP status codes, attribute routing, and JSON serialization, without any of WCF's SOAP-oriented configuration overhead. In modern .NET development, ASP.NET Core Web API is unambiguously the recommended choice for any new RESTful API — WCF (including WCF REST) is considered legacy and isn't even supported on .NET Core/.NET 5+ (CoreWCF exists as a community-maintained port for migration scenarios, but new REST development shouldn't start there). The historical progression (ASMX → WCF → WCF REST → ASP.NET Web API → ASP.NET Core Web API) reflects Microsoft's gradual shift from SOAP-first, protocol-agnostic service frameworks toward a purpose-built, HTTP-native REST framework as REST became the dominant industry style. Understanding this history is useful mainly for maintaining or migrating legacy enterprise systems still running WCF services, since virtually all new API development today targets ASP.NET Core Web API directly.

```csharp
// WCF REST (legacy): action exposed via WebInvoke over webHttpBinding
[WebInvoke(Method = "GET", UriTemplate = "orders/{id}")]
Order GetOrder(string id);

// ASP.NET Core Web API (modern): purpose-built for REST
[HttpGet("{id}")]
public async Task<ActionResult<Order>> GetOrder(int id) => Ok(await _service.GetAsync(id));
```

---


## Enlist some important constraints for RESTful web services
REST is defined by six architectural constraints, and satisfying all of them (except the optional one) is what technically qualifies a service as truly RESTful. **Client-server separation** requires the UI and data storage concerns to be independently evolvable, so a mobile app and a web app can consume the same backend without either side dictating the other's implementation. **Statelessness** requires every request to carry all necessary context, with no client session state stored on the server between calls. **Cacheability** requires responses to explicitly (or implicitly, by convention) indicate whether they can be cached, enabling clients and intermediaries to reuse data and reduce server load. **Uniform interface** is the most defining constraint, itself broken into four sub-constraints: identification of resources (via URIs), manipulation through representations (a client can modify a resource by sending a new representation, e.g., via PUT), self-descriptive messages (each message includes enough information — like `Content-Type` — to be understood on its own), and HATEOAS (hypermedia links guiding the client to related actions/resources). **Layered system** requires that a client cannot necessarily tell whether it's talking directly to the origin server or through intermediary layers (load balancers, gateways, caches), enabling infrastructure like Azure API Management or a CDN to be inserted transparently. **Code-on-demand** is the one optional constraint, allowing servers to extend client functionality by transmitting executable code (e.g., JavaScript), rarely used explicitly as a "REST feature" in typical API design today. In practice, most production APIs (including typical ASP.NET Core Web APIs) satisfy the first five constraints reasonably well while skipping full HATEOAS, which is generally accepted as sufficiently RESTful for real-world purposes.

```csharp
// Layered system: API Management/gateway can sit transparently in front of this controller
[ApiController]
[Route("api/orders")]
public class OrdersController : ControllerBase {
    [HttpGet("{id}")]
    public async Task<ActionResult<Order>> Get(int id) => Ok(await _service.GetAsync(id));
}
```

---


## What are the best practices to be followed while designing a secure RESTful web service?
Always enforce HTTPS/TLS for every endpoint (never allow plain HTTP in production) to protect credentials, tokens, and payload data from interception, and use `UseHttpsRedirection()`/HSTS in ASP.NET Core to enforce this at the framework level. Authenticate every request statelessly using short-lived JWT bearer tokens (ideally signed with RS256 so the resource server only needs the public key) rather than server-side sessions, and pair this with proper authorization (role- or policy-based `[Authorize]` attributes) so authenticated users can only access resources/actions they're actually permitted to. Validate and sanitize all input at the API boundary — using model validation attributes (`[Required]`, `[StringLength]`) and rejecting malformed requests early — to prevent injection attacks (SQL injection via parameterized queries/EF Core, XSS via output encoding/`HtmlSanitizer` for any rendered HTML). Apply rate limiting/throttling (built-in ASP.NET Core rate limiting middleware, or Azure API Management policies) to prevent abuse, brute-force attempts, and denial-of-service patterns, and never expose verbose internal error details (stack traces, SQL error messages) to clients — return generic, safe error messages while logging full details server-side (Application Insights). Avoid exposing internal implementation details in URIs or payloads (e.g., don't leak database auto-increment IDs if they reveal record counts/business volume; consider GUIDs for sensitive resources), and always use the principle of least privilege for any credentials/connection strings, storing secrets in Azure Key Vault rather than config files or source control. Enable CORS carefully with an explicit allow-list of trusted origins rather than a wildcard (`*`) whenever credentials or sensitive data are involved, since a wildcard combined with credentialed requests is a serious security gap. Finally, keep dependencies patched and regularly scanned for known vulnerabilities (NuGet package auditing, Dependabot/GitHub security alerts), since outdated libraries are one of the most common real-world attack vectors even in an otherwise well-designed API.

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options => {
        options.RequireHttpsMetadata = true;
        options.TokenValidationParameters = new TokenValidationParameters {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            IssuerSigningKey = rsaPublicKey
        };
    });

var app = builder.Build();
app.UseHttpsRedirection();
app.UseAuthentication();
app.UseAuthorization();
```

---


## Name some best practices for better RESTful API design
Design URIs around nouns/resources, not actions (`/api/orders/{id}` rather than `/api/getOrder?id={id}`), and use HTTP verbs to express the operation, keeping the API predictable and consistent across all endpoints. Use plural nouns for collections consistently (`/api/customers`, `/api/orders`) and nest sub-resources logically but sparingly (2-3 levels deep max, e.g., `/api/customers/{id}/orders`) to avoid overly rigid, brittle URI hierarchies. Return correct, meaningful HTTP status codes rather than always returning `200 OK` with an error flag in the body — use `201 Created` with a `Location` header for successful creation, `204 No Content` for successful operations with no body, `400 Bad Request` for validation errors, `401`/`403` for authentication/authorization failures, and `404 Not Found` for missing resources. Support pagination, filtering, and sorting via query parameters for large collections (`?page=2&pageSize=50&sort=-createdDate`) rather than returning unbounded result sets, which protects both server performance and client responsiveness. Version your API deliberately from day one (URI versioning like `/api/v1/orders`, or header-based versioning) so breaking changes can be introduced without disrupting existing consumers, and document the API thoroughly using OpenAPI/Swagger (Swashbuckle in ASP.NET Core) so it's self-describing and easy to explore. Use consistent, structured error responses (RFC 7807 Problem Details is the modern standard, built into ASP.NET Core) so clients can reliably parse and handle errors programmatically rather than guessing based on inconsistent ad hoc error shapes. Favor idempotent design wherever possible (supporting safe retries for `PUT`/`DELETE`, and idempotency keys for `POST` where duplicate submissions are a risk), and always design with statelessness and horizontal scalability in mind from the start rather than retrofitting it later once the API is already load-bearing in production.

```csharp
[HttpGet]
public async Task<ActionResult<PagedResult<Order>>> GetOrders(
    [FromQuery] int page = 1, [FromQuery] int pageSize = 50, [FromQuery] string? sort = null) {
    var orders = await _service.GetPagedAsync(page, pageSize, sort);
    return Ok(orders);
}
```
