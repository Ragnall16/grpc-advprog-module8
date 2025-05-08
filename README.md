# Reflection Modul 8
Ragnall Muhammad Al Fath
2306210550 / AdPro B
---

### 1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
Unary RPC: Single request, single response (like ProcessPayment). Best for simple, synchronous operations where you need a complete response immediately.

Server Streaming RPC: Single request, multiple responses (like GetTransactionHistory). Ideal for returning large datasets, real-time updates, or scenarios where data becomes available over time.

Bi-directional Streaming: Multiple requests and responses in any order (like Chat). Suitable for real-time communication, long-lived connections, or when both client and server need to send messages independently.

### 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
Authentication: Implement TLS certificates for transport security

Authorization: Add middleware for role-based access control

Encryption: Use mTLS for mutual authentication

Token validation: Implement JWT or OAuth2 token validation

Interceptors: Add Rust interceptors to handle 
security concerns centrally

Input validation: Validate all incoming requests to prevent injection attacks

### 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
Connection management: Handling disconnections gracefully

Resource leaks: Ensuring streams are properly closed

Error handling: Propagating errors across the stream

Ordering: Maintaining message order when needed

Backpressure: Managing memory when clients send data faster than can be processed

Thread safety: Coordinating across multiple async tasks safely

Testing: Properly testing streaming behavior is complex

### 4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
**Advantages:**

Integrates well with Tokio's async ecosystem

Handles backpressure automatically

Provides clean abstraction over message passing

**Disadvantages:**

Adds memory overhead from buffering

May introduce additional complexity in debugging

Limited control over stream internals

Potential blocking when buffer fills

### 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
A well-structured Rust gRPC codebase should separate service implementations into distinct modules to maintain clear boundaries. Business logic should be extracted from RPC handlers, allowing them to focus solely on mapping requests and responses. Using traits for defining service behaviors promotes flexibility and testing. Creating dedicated data access layers isolates persistence concerns from service logic. Implementing middleware patterns through interceptors enables cross-cutting concerns like logging or authentication to be handled uniformly. Shared utility functions can reduce duplication across services, while configuration-driven initialization makes the system adaptable to different environments without code changes. This approach creates a maintainable architecture that can evolve alongside business requirements.

### 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
A production-ready payment service requires comprehensive validation logic for payment details, ensuring amounts, account numbers, and other credentials meet requirements. Transaction logging is essential for audit trails and compliance purposes. Integration with external payment gateways would be necessary, alongside proper error handling for gateway failures. Concurrency controls prevent race conditions when multiple payments affect the same account. Retry mechanisms should be implemented for failed transactions, along with idempotency keys to prevent duplicate processing. More sophisticated error reporting would help with troubleshooting and customer support. Finally, fraud detection algorithms would analyze transaction patterns to identify suspicious activity, enhancing security while maintaining a smooth user experience.

### 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
Adopting gRPC fundamentally shapes distributed system architecture by enforcing stricter interface definitions through Protocol Buffers, creating clear contracts between services. This naturally encourages a service-oriented or microservices approach with well-defined boundaries. However, interoperability challenges arise when integrating with systems that don't support gRPC natively, often requiring gateway services to translate between protocols. Browser-based clients typically need additional components like grpc-web proxies to communicate with gRPC backends. Despite these challenges, gRPC enables more efficient communication between services through features like multiplexing and binary serialization, reducing latency and bandwidth usage. The strong typing across service boundaries also catches integration issues earlier in the development cycle, leading to more robust distributed systems overall.

### 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
**HTTP/2 advantages:**

Multiplexing requests over single connection

Header compression

Binary protocol is more efficient

Server push capabilities

Better connection utilization


**Disadvantages:**

More complex implementation

Less human-readable for debugging

Often requires TLS

Less universal tooling support

Greater complexity in server configuration

### 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
REST: Request-response model requires polling or webhooks for updates

gRPC: Bidirectional streams enable real-time updates without polling

REST: Higher latency due to connection setup per request

gRPC: Lower latency with persistent connections and multiplexing

REST: Simpler client implementation for basic scenarios

gRPC: Better support for event-based communication patterns

### 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
Protocol Buffers: Strongly typed, contract-based API evolution

JSON: More flexible schema evolution but less type safety

Protocol Buffers: Smaller payload size and faster serialization/deserialization

JSON: Human-readable, easier debugging

Protocol Buffers: Require code generation step

JSON: Universally supported, no special tooling needed

Protocol Buffers: Better performance at scale