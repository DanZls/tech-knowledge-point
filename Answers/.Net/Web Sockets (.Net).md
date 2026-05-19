# Entry

## Q1: What is WebSockets?

WebSockets is a protocol providing full-duplex communication channels over a single, long-lived TCP connection. Unlike HTTP, which is unidirectional and request-response based, WebSockets allows messages to be sent in both directions at any time, enabling real-time, interactive communication between client and server. WebSockets are standardized as RFC 6455 and can be implemented in web browsers and servers. The protocol starts with an HTTP handshake, then upgrades to a persistent connection using a specific WebSocket handshake. This mechanism is often used for live applications like chat, gaming, financial tickers, and collaborative editing, where low-latency updates are crucial.

```csharp
// Creating a WebSocket client connection in .NET
using System.Net.WebSockets;
using System.Threading.Tasks;

public class WebSocketExample
{
    public async Task ConnectAsync()
    {
        using (var ws = new ClientWebSocket())
        {
            await ws.ConnectAsync(new Uri("wss://example.com/socket"), CancellationToken.None);
            // WebSocket now open, can send and receive messages
        }
    }
}
```
---

# Junior

## Q2: Why use WebSocket over HTTP?

WebSockets are used over HTTP when applications require low-latency, real-time bi-directional communication. HTTP is request-response based, so after each request, the connection is typically closed, and any updates from the server must be polled by the client. This increases latency and network traffic. WebSockets, on the other hand, maintain a persistent connection, allowing both the server and client to send messages independently at any time. This design is more efficient for live chat, gaming, stock tickers, or collaborative tools since updates are delivered instantly and resource usage is minimized as connections are reused.

```csharp
// WebSocket vs HTTP: WebSocket enables real-time send/receive without repeating HTTP requests.
```
---

## Q3: Explain what is Server-Sent Events (SSE) / EventSource?

Server-Sent Events (SSE) is a server push technology enabling servers to send automatic updates to clients over a single HTTP connection. Unlike WebSockets, communication is one-way: only the server can send messages to the browser. SSE uses the text/event-stream MIME type and is typically accessed using JavaScript's EventSource API. It's simpler than WebSockets for pushing updates like notifications, feeds, or logs to the client, but does not support client-to-server communication besides the initial request.

```csharp
// C# backend: writing SSE data to response
public async Task SendSse(HttpResponse response)
{
    response.ContentType = "text/event-stream";
    await response.WriteAsync("data: Hello world\n\n");
    await response.Body.FlushAsync();
}
```
---

## Q4: What is Short Polling and what problems do we have with it?

Short Polling is a technique where the client repeatedly sends HTTP requests to the server at fixed intervals to check for updates. Each request is handled independently, typically resulting in an HTTP response regardless of whether there’s new data. The drawbacks include increased network and server resource usage due to frequent requests, higher latency for real-time updates, and poor scalability. It can also lead to delayed or missed updates if polling intervals are too large.

```csharp
// Client (pseudo-code): repeatedly fetches updates every 2 seconds.
while (true)
{
    var response = await httpClient.GetAsync("api/updates");
    await Task.Delay(2000);
}
```
---

## Q5: What do you mean by lower latency interaction?

Lower latency interaction means reducing the delay between when an event occurs on the server and when the client receives it. It’s critical in scenarios like online gaming, chat, live feeds, and financial trading, where delays degrade the user experience or cause issues. WebSockets, for instance, enable lower latency compared to HTTP polling because the connection stays open and data is pushed as soon as it’s ready, rather than waiting for the client to request updates.

```csharp
// WebSockets push updates instantly, reducing delay:
await webSocket.SendAsync(buffer, WebSocketMessageType.Text, true, CancellationToken.None);
```
---

# Mid

## Q6: Name and explain what different communication techniques on the web do you know?

Common web communication techniques include:

- HTTP Polling: Client repeatedly requests data at intervals.
- Long Polling: Client requests and waits; server responds only when data is available or timeout occurs.
- Server-Sent Events (SSE): Server pushes updates to the client via HTTP stream.
- WebSockets: Persistent, full-duplex connection for real-time updates in both directions.
- AJAX: Asynchronous HTTP requests, often used for dynamic content.
- HTTP2 Push: Server can push resources proactively.
Different techniques balance reliability, latency, scalability, and complexity, with WebSockets and SSE specialized for real-time scenarios.

```csharp
// Example: Initiating WebSocket and Long Polling (conceptually)
if (supportsWebSockets)
{
    // Use WebSocket
}
else
{
    // Fallback to Long Polling
}
```
---

## Q7: WebSockets vs Rest API for real time data? Which to choose?

For real-time data, WebSockets are usually preferred over REST APIs. REST APIs operate on HTTP and are ideal for stateless, transactional operations—clients must poll or refresh to get updates, which introduces latency and resource waste. WebSockets keep a persistent connection, allowing immediate data push from server to client, resulting in true low-latency real-time updates. Choose WebSockets for chat, live dashboards, streaming, or online collaboration. Use REST APIs for CRUD operations, configuration, or when state synchronization and connection persistence aren’t needed.

```csharp
// WebSocket: Best for instant data updates (e.g., chat app)
// REST API: Best for discrete requests and not live data
```
---

## Q8: Explain what is Long Polling?

Long Polling is a technique where the client sends an HTTP request to the server, which holds the connection open until new data is available or a timeout occurs. When the server responds, the client immediately makes another request, creating a near-real-time illusion. Unlike short polling, long polling reduces unnecessary requests but still requires a new connection for each response, increasing overhead compared to truly persistent connections like WebSockets.

```csharp
// Pseudo C# example: client waits for server's response, then re-requests
while (true)
{
    var response = await httpClient.GetAsync("api/longpoll");
    // Handle response...
}
```
---

## Q9: Mention some advantages of SSE over WebSockets

Server-Sent Events (SSE) are simpler to implement for one-way (server-to-client) notifications or streaming—it uses HTTP, works well with existing infrastructure, supports automatic reconnection, and is natively supported in browsers. SSE inherently supports text-based data, is easier to debug, and traverses firewalls/proxies more reliably. For server-only push scenarios such as news feeds or live notifications, SSE is often preferred over the more complex WebSocket, which is bidirectional and may require additional handling for message protocol, ping/pong, etc.

```csharp
// SSE (HTTP text/event-stream) is built on standard HTTP and simple to set up.
```
---

## Q10: Explain key features of Socket.io

Socket.io is a JavaScript library for real-time web applications. Its key features include:

- Automatic fallback from WebSockets to long polling or other transports for best compatibility.
- Event-driven architecture supporting custom and predefined events (e.g., 'connect', 'message', 'disconnect').
- Room and namespace support for scalable group and private communication.
- Built-in reconnection logic and heartbeat.
- Supports broadcasting and message acknowledgement.
Socket.io simplifies real-time communication by abstracting transport details and providing a robust API.

```csharp
// Socket.io handles fallback, reconnection, rooms, and broadcasting (JavaScript-based).
```
---

## Q11: What is the difference between WebSockets vs. Server-Sent Events/EventSource?

The key difference is bidirectionality: WebSockets provide full-duplex communication, where both client and server can independently send messages at any time. Server-Sent Events (SSE), in contrast, are one-way; only the server can push updates to the client after the initial HTTP request. WebSockets work with any kind of data (binary/text), while SSE is typically text-based and easier to implement but limited to server-to-client events. WebSockets are suitable for chat, gaming, or collaborative editing, while SSE is best for live feeds, notifications, or log streaming.

```csharp
// WebSockets: send/receive messages both ways
// SSE: server streams events to client (one-way)
```
---

# Senior

## Q12: What are the differences between Socket.io and WebSockets?

Socket.io is a higher-level abstraction built on top of WebSockets that adds additional features such as automatic reconnection, fallback transports (like long polling), broadcasting, and event-based communication. WebSockets is a protocol that provides full-duplex communication over a single TCP connection but does not define features for reconnection or event-based messaging — it's just a transport. Socket.io can work over WebSocket where available but will transparently fall back to HTTP long polling or other methods when WebSocket is unavailable, providing better browser compatibility and reliability. Additionally, Socket.io has a richer API, supports namespaces and rooms (for message grouping), and can handle complex use-cases out of the box. WebSocket, being a protocol, is less feature-rich but is lighter and more closely tied to the network stack.

```csharp
// Basic WebSocket usage in C#
using System.Net.WebSockets;
using System.Threading;
using System.Threading.Tasks;

public async Task UseWebSocketExample()
{
    using (var ws = new ClientWebSocket())
    {
        await ws.ConnectAsync(new Uri("wss://echo.websocket.org"), CancellationToken.None);
        // Send and receive data directly
    }
}

// With Socket.IO on .NET (package required), you'd use abstractions like:
var socket = IO.Socket("https://yoursocketioserver");
socket.On("message", data => { /* handle message */ });
```
---

## Q13: What is Sec-WebSocket-Key for?

The `Sec-WebSocket-Key` is a unique, randomly generated base64-encoded value sent from the client to the server during the WebSocket handshake. Its main purpose is to prevent malicious connections and to ensure that the server speaks the WebSocket protocol, not just interpreting HTTP requests incorrectly. The server takes this key, concatenates it with a globally defined GUID (`258EAFA5-E914-47DA-95CA-C5AB0DC85B11`), hashes it using SHA-1, and returns the result in the `Sec-WebSocket-Accept` header. This proves to the client that the server understood the protocol negotiation.

```csharp
// Key creation (client-side, handled by browser/WS library):
string secWebSocketKey = Convert.ToBase64String(Guid.NewGuid().ToByteArray());

// Server response:
string acceptKey = Convert.ToBase64String(
    SHA1.Create().ComputeHash(
        Encoding.UTF8.GetBytes(secWebSocketKey + "258EAFA5-E914-47DA-95CA-C5AB0DC85B11")
    )
);
```
---

## Q14: Why would you choose Server-Sent Events over WebSockets?

Server-Sent Events (SSE) is a simpler API for unidirectional messaging (from server to client) and is often chosen for its simplicity when only server-to-client updates are required. SSE works over standard HTTP, supports automatic reconnection, and is natively supported by browsers with straightforward JavaScript usage, making infrastructure setup easier. SSE aligns well with HTTP semantics, proxies, and firewalls and can reuse authentication and compression mechanisms. For use cases like live news or stock tickers, where only the server needs to push data, SSE can be easier to scale and maintain.

```csharp
// SSE is not native to .NET,
// but you can implement it with an MVC Controller like this:
public IActionResult StreamExample()
{
    Response.ContentType = "text/event-stream";
    while (true)
    {
        Response.WriteAsync($"data: {DateTime.Now}\n\n");
        Response.Body.Flush();
        Thread.Sleep(1000);
    }
}
```
---

## Q15: Explain how does WebSockets protocol work under the hood

The WebSockets protocol upgrades an HTTP connection via a handshake to allow for full-duplex communication. The client sends an HTTP `Upgrade: websocket` request including the `Sec-WebSocket-Key`, and if the server supports WebSockets, it replies with an HTTP 101 status code, with `Upgrade` and `Sec-WebSocket-Accept` headers. After this handshake, both client and server can asynchronously send messages to each other in the form of WebSocket frames, which can be text or binary. The connection remains open, reducing the overhead of establishing new TCP connections. Automatic ping/pong frames maintain the connection health.

```csharp
// WebSocket handshake (pseudo code):
// Client:
GET /chat HTTP/1.1
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==

// Server:
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
```
---

## Q16: What is WebSockets Frame?

A WebSocket frame is a defined data packet in the WebSocket protocol, encapsulating either text or binary data to be sent between the client and server. Each frame contains control flags, the payload length, masking key (for security reasons on the client-to-server direction), and the actual data payload. The framing allows messages to be fragmented and sent in pieces if needed, or grouped. Frame types include text, binary, ping, pong, and close operations, allowing control as well as data transfer.

```csharp
// Reading frames via .NET API (simplified)
var buffer = new byte[1024];
WebSocketReceiveResult result = await ws.ReceiveAsync(new ArraySegment<byte>(buffer), CancellationToken.None);
if (result.MessageType == WebSocketMessageType.Text)
{
    string message = Encoding.UTF8.GetString(buffer, 0, result.Count);
}
```
---

## Q17: When to use WebRTC over WebSockets?

WebRTC is best used when you need secure, low-latency, peer-to-peer communication with direct media (audio/video/file) streaming capabilities. It supports NAT traversal, media encoding/decoding, and works in browsers without plugins. While WebSockets is ideal for full-duplex text-based or binary messaging between clients and servers, WebRTC excels for real-time, high-bandwidth scenarios like video chat, live audio streaming, or direct data sharing between users. If complex signaling, server relay, or media transport is needed, choose WebRTC.

```csharp
// WebRTC not native to C#, but signaling often via WebSockets:
socket.On("offer", (data) => { /* handle WebRTC offer, then connect peers */ });
```
---

## Q18: Would WebSockets be able to handle 1,000,000 concurrent connections?

Technically, WebSockets can handle large numbers of concurrent connections, but doing so at the 1,000,000 level is challenging and requires careful infrastructure design. The main issues include OS limits on open file/socket descriptors, memory usage per connection, and handling context switching. Specialized event-driven servers, efficient async I/O (like .NET's async/await), connection sharding across many servers, and use of load balancers are needed for scalability. Application design (stateless, distributed), proper monitoring, and tuning the OS (like increasing the maximum open files on Linux) are also crucial.

```csharp
// Hosting many WebSockets with async server code (simplified skeleton)
public async Task ListenWebSocketsAsync()
{
    TcpListener listener = new TcpListener(IPAddress.Any, 8080);
    listener.Start();
    while (true)
    {
        TcpClient client = await listener.AcceptTcpClientAsync();
        _ = HandleWebSocketAsync(client); // fire-and-forget, handle concurrently
    }
}
```
---

## Q19: Can you suggest how to load balance Web Sockets?

To load balance WebSockets, you usually use a Layer 4 (TCP) or Layer 7 (Application/HTTP) load balancer configured for sticky sessions ("session affinity"), ensuring a client stays on the same backend server after the initial upgrade handshake. Examples include NGINX, HAProxy, Azure Application Gateway, or AWS Elastic Load Balancer. The load balancer must support HTTP upgrades and TCP proxying. To scale further, you can share session state between nodes via a distributed cache (like Redis), or architect stateless message processing.

```csharp
// NGINX WebSocket sample config
// proxy_pass http://backend_servers;
// proxy_set_header Upgrade $http_upgrade;
// proxy_set_header Connection "upgrade";
```
---

## Q20: What are pros and cons of Azure Web PubSub vs SignalR?

Azure Web PubSub and Azure SignalR are services for real-time messaging, but they differ in integration and feature set. Web PubSub is protocol-agnostic, supports native WebSockets with custom protocols, and is best for custom client/server implementations, IoT, or when direct WebSocket control is needed. SignalR adds abstractions like hubs, groups, user management, and automatic fallback to polling if necessary, making it better for .NET-centric apps or quick real-time features. PubSub is more flexible and scalable but less "batteries-included" than SignalR, which is more opinionated and tightly integrated with ASP.NET.

```csharp
// SignalR (server-side hub)
public class ChatHub : Hub
{
    public async Task SendMessage(string message)
    {
        await Clients.All.SendAsync("ReceiveMessage", message);
    }
}

// Web PubSub: lower-level message send via REST/WS API
```
---

## Q21: What is the fundamental difference between WebSockets and pure TCP?

WebSockets is a protocol on top of TCP that enables bidirectional communication inside a web-friendly, firewall/NAT-safe and HTTP-compatible envelope. It starts as HTTP and upgrades to a persistent socket, defining framing, subprotocol negotiation, and masking for security. Pure TCP is just a byte-stream with no message boundaries or agreed higher-level protocol; it’s not web-browser compatible and not aware of HTTP handshakes. WebSockets leverages TCP for transport, but adds message framing, security, and compatibility for web use.

```csharp
// TCP client (low-level, no message envelopes)
TcpClient client = new TcpClient("server", 8000);
NetworkStream stream = client.GetStream();
stream.Write(bytes, 0, bytes.Length);

// WebSocket client (protocol-level, handled by library)
ClientWebSocket ws = new ClientWebSocket();
await ws.ConnectAsync(new Uri("wss://host/ws"), CancellationToken.None);
```
---

# Expert

## Q22: What is the mask in a WebSocket frame?

The mask is a 4-byte random value required in every frame sent from the browser (client) to the server. It's used to XOR the payload data, preventing proxy cache poisoning and ensuring that intermediate infrastructure cannot inadvertently or maliciously inject/preload cached data as WebSocket frames. The server unmasks received data using this mask and processes the original payload. Server-to-client frames are not masked to reduce resource usage.

```csharp
// Pseudocode to unmask WebSocket frame
for (int i = 0; i < payload.Length; i++)
{
    payload[i] ^= maskingKey[i % 4];
}
```
---

## Q23: Explain why CDN (in)availability may be a problem for using WebSockets?

Many CDNs are built for cacheable, stateless HTTP traffic, and not all support HTTP upgrades or persistent connections required by WebSockets. If a CDN sits between the client and backend and doesn't support WebSocket proxying, connection upgrades may fail or be dropped, leading to failures in establishing WebSocket connections. Even when supported, CDNs may have idle timeouts, limited sticky-session capabilities, or insufficient support for handling millions of concurrent, long-lived connections, making them problematic for WebSocket traffic.

```csharp
// On CDN config, ensure support for HTTP Upgrade header:
// allow-upgrade: websocket
// timeout: suitably high
```
---

## Q24: How to use CHAP Authentication (Challenge Response Authentication) for webSockets?

To use CHAP with WebSockets, implement a custom handshake or message exchange after establishing the WebSocket connection. The server issues a challenge (a random nonce) after the connection opens; the client hashes this nonce with its secret (like password) and sends the hash back. The server validates the hash using its own knowledge of the secret and the same algorithm. Since WebSockets itself does not define authentication, this must be part of the app protocol after the handshake.

```csharp
// On connection open:
// 1. Server sends nonce
// 2. Client computes hash = Hash(nonce + password) and sends to server
// 3. Server checks; if correct, continues

// Client side:
string hash = Hash(nonce + password);
await ws.SendAsync(new ArraySegment<byte>(Encoding.UTF8.GetBytes(hash)), WebSocketMessageType.Text, true, CancellationToken.None);
```
---

## Q25: How would you secure WebSockets communication on your project?

Use secure WebSocket (`wss://`) to encrypt all traffic with TLS. Authenticate users before allowing upgrades or via a custom protocol after connection (e.g., tokens or CHAP). Use strong CORS rules and restrict origins. Always validate and sanitize input messages to prevent injection attacks, and use access controls to prevent unauthorized access. Make sure to handle DOS and resource exhaustion by setting limits on connections and message sizes, and keep WebSocket server libraries up to date.

```csharp
// Server configuration for wss://
var host = new WebHostBuilder()
    .UseKestrel(opts => opts.Listen(IPAddress.Any, 443, listenOpts => {
        listenOpts.UseHttps("cert.pfx", "password");
    }))
    .UseStartup<Startup>()
    .Build();
host.Run();
```
---

## Q26: How can WebSockets be better than Long-Polling in terms of performance?

WebSockets establish a single, persistent TCP connection for bi-directional communication, eliminating the overhead of repeated HTTP request/response cycles present in long-polling. This reduces latency, network and server load, and improves real-time responsiveness since data can be pushed as soon as it’s available. Fewer HTTP headers are sent, and connection setup costs are only paid once, resulting in reduced bandwidth consumption and faster message delivery compared to re-establishing connections for each long-poll poll.

```csharp
// WebSocket: single, persistent connection
await ws.ConnectAsync(uri, CancellationToken.None);
await ws.SendAsync(...);
await ws.ReceiveAsync(...);

// Long-polling: repeated connections
while (true)
{
    var response = await httpClient.GetAsync("server/long-poll");
    // process response data, then repeat
}
```
---