# Backend Engineering Learning Path

This path is for a complete beginner who wants to build the server side of applications. Backend engineers receive requests, enforce business rules, protect data, coordinate databases and other services, perform background work, and keep systems observable and recoverable after deployment.

Backend development is not only creating routes that return JSON. A useful service also needs clear contracts, runtime validation, authorization, transactions, concurrency control, testing, logging, monitoring, secure configuration, deployment, and a safe way to change behavior over time.

## What is available now

The repository already contains the shared language and tool foundations:

- [Git](../learn-to-git/README.md) teaches safe history, collaboration, automation, investigation, release tags, and recovery.
- [SQL](../learn-to-sql/README.md) teaches relational modeling, transactions, indexes, migrations, concurrency, PostgreSQL, least privilege, and performance.
- [TypeScript](../learn-to-typescript/README.md), [Python](../learn-to-python/README.md), [Go](../learn-to-go/README.md), [Java](../learn-to-java/README.md), and [Rust](../learn-to-rust/README.md) are available as primary language choices.
- [Backend Foundations](../learn-to-backend-foundations/README.md) teaches the shared server responsibilities before framework-specific implementation.
- Complete implementation courses are available for [Node.js and TypeScript](../learn-to-nodejs-backend/README.md), [Python](../learn-to-python-backend/README.md), [Go](../learn-to-go-backend/README.md), [Java and Spring](../learn-to-java-spring-backend/README.md), and [Rust](../learn-to-rust-backend/README.md).

After the shared prerequisites, complete Backend Foundations and exactly one primary implementation course. A second language is optional later.

## Start with Git

Complete Git Modules 01 through 13 before beginning a large server project. Return to Modules 14 through 29 while the project gains branches, releases, automated checks, and history worth investigating.

## Choose one primary language

You do not need five backend languages. Choose one branch and become comfortable with it before comparing another.

### TypeScript and Node.js branch

1. Complete the entire [TypeScript course](../learn-to-typescript/README.md).
2. Complete the entire [SQL course](../learn-to-sql/README.md).
3. Complete [Backend Foundations](../learn-to-backend-foundations/README.md).
4. Complete [Node.js and TypeScript Backend Development](../learn-to-nodejs-backend/README.md).

This branch is for API services, realtime systems, server-rendered applications, and teams that share TypeScript between clients and servers. React and Next.js are not prerequisites for a backend-only TypeScript learner. Next.js remains a full-stack specialization in the [Web Development path](web-development.md).

### Python branch

1. Complete [Python](../learn-to-python/README.md) Modules 01 through 32.
2. Complete [SQL](../learn-to-sql/README.md) Modules 01 through 23.
3. Complete Python Modules 33 through 38.
4. Complete SQL Modules 24 through 34.
5. Complete [Backend Foundations](../learn-to-backend-foundations/README.md).
6. Complete [Python Backend Development](../learn-to-python-backend/README.md).

This order prevents Python's database module from appearing before the required SQL foundation. The specialization should teach the server interface and HTTP directly before using FastAPI for an API-first implementation. Django can be a later full web application branch. Learners do not need both frameworks at once.

### Go branch

1. Complete [Go](../learn-to-go/README.md) Modules 01 through 28.
2. Complete [SQL](../learn-to-sql/README.md) Modules 01 through 23.
3. Complete Go Modules 29 through 34.
4. Complete SQL Modules 24 through 34.
5. Complete [Backend Foundations](../learn-to-backend-foundations/README.md).
6. Complete [Go Backend Development](../learn-to-go-backend/README.md).

The existing Go course already introduces HTTP clients, servers, middleware, context, cancellation, and testing. The backend specialization should begin with the standard library and add a router or framework only when it provides a clear benefit.

### Java branch

1. Complete [Java](../learn-to-java/README.md) Modules 01 through 30.
2. Complete [SQL](../learn-to-sql/README.md) Modules 01 through 23.
3. Complete Java Modules 31 through 40.
4. Complete SQL Modules 24 through 34.
5. Complete [Backend Foundations](../learn-to-backend-foundations/README.md).
6. Complete [Java and Spring Backend Development](../learn-to-java-spring-backend/README.md).

This order teaches SQL before JDBC, connection pools, and transactions. The server specialization should introduce Spring Boot and Spring MVC after plain Java dependencies, HTTP clients, JSON boundaries, and tests are understood.

### Rust branch

1. Complete the entire [Rust course](../learn-to-rust/README.md).
2. Complete the entire [SQL course](../learn-to-sql/README.md).
3. Complete [Backend Foundations](../learn-to-backend-foundations/README.md).
4. Complete [Rust Backend Development](../learn-to-rust-backend/README.md).

The existing Rust course teaches ownership, errors, Serde, asynchronous work, Tokio, networking, testing, and security boundaries. The specialization should use the runtime and HTTP layers deliberately before adding an ergonomic web framework such as Axum.

### Where C fits

[C](../learn-to-c/README.md) is valuable for understanding memory, operating systems, native libraries, and performance-sensitive infrastructure. It is not a recommended first backend application branch for a complete beginner because the repository already offers safer and more productive server languages. C can become a later systems specialization.

## Shared backend sequence

Every language specialization should preserve this concept order even though its syntax, libraries, and module count will differ.

### Stage 1: Server, Network, and HTTP Foundations

Learn processes, ports, sockets, clients, servers, DNS, TLS, proxies, URLs, HTTP methods, headers, bodies, content types, status codes, caching semantics, cookies, and command-line request tools. Build one small server with the language's basic server facilities before depending on a large framework.

You should be able to inspect a raw request and explain which behavior comes from HTTP, which comes from the framework, and which belongs to application code.

### Stage 2: Routing, Middleware, and Application Structure

Learn route matching, handlers, middleware order, dependency boundaries, configuration, startup, graceful shutdown, request-scoped state, cancellation, and separation between transport code, business rules, and data access.

Begin with a modular monolith. A folder structure does not need a complex architecture name to keep responsibilities separate.

### Stage 3: API Contracts and Runtime Validation

Learn resource design, request and response schemas, field validation, error formats, pagination, filtering, sorting, file uploads, content negotiation, idempotency keys, webhooks, compatibility, deprecation, and OpenAPI documents.

Types in source code do not validate network input. Every path value, query value, header, body, file, and upstream response remains untrusted at runtime.

REST over HTTP should be learned first. GraphQL, gRPC, WebSockets, and server-sent events are later choices for problems that need them, not required replacements for a clear HTTP API.

### Stage 4: Relational Persistence and Transactions

Use PostgreSQL as the main production relational database after SQLite practice. Learn connection pools, parameterized queries, repositories, migrations, transaction boundaries, isolation, locking, optimistic concurrency, pagination, query plans, backups, and restoration.

Teach SQL directly before an object-relational mapper. An ORM can reduce repetitive mapping, but it cannot choose correct indexes, transaction boundaries, or data models automatically.

### Stage 5: Identity, Sessions, and Authorization

Separate authentication from authorization. Learn password storage through maintained libraries, secure cookies, server sessions, token validation, account recovery, multi-factor authentication concepts, OAuth and OpenID Connect roles, roles and permissions, resource ownership, tenant isolation, CSRF, CORS, rate limits, and audit records.

Every protected operation must enforce authorization on the server. Hiding a button or checking only the route is not protection.

### Stage 6: External Services, Caching, and Background Work

Learn outbound HTTP ownership, timeouts, retries with backoff, circuit breaking, bulkheads, rate limits, response validation, caching, cache invalidation, queues, workers, scheduled jobs, dead-letter handling, idempotent consumers, and transactional outbox concepts.

Retries must consider whether an operation is safe to repeat. Background work must expose status and failure instead of disappearing after a request ends.

### Stage 7: Testing, Concurrency, and Reliability

Build unit tests for business rules, integration tests for database and HTTP boundaries, contract tests for APIs, and end-to-end tests for critical flows. Learn test data isolation, deterministic time, failure injection, race detection, load testing, cancellation, resource limits, and graceful degradation.

Mocks should replace boundaries a test does not own. They should not make every database, network, and concurrency failure impossible.

### Stage 8: Security Engineering

Apply secure defaults throughout the earlier stages, then study threat modeling, injection, broken object authorization, server-side request forgery, unsafe file handling, request smuggling concepts, secret management, dependency risk, denial of service, data minimization, encryption boundaries, security headers, incident evidence, and coordinated patching.

Framework defaults help, but application authorization and business abuse controls remain the developer's responsibility.

### Stage 9: Observability and Performance

Learn structured logs, correlation identifiers, metrics, traces, context propagation, service-level indicators, alerts, health and readiness checks, profiling, query analysis, capacity tests, and privacy-aware telemetry. Use OpenTelemetry after the meaning of logs, metrics, and traces is clear.

Measure before optimizing. A low average response time can still hide slow percentiles, failed requests, overloaded dependencies, or incorrect cached data.

### Stage 10: Packaging, Deployment, and Operations

Build a production artifact, run it as a non-root process, handle termination, validate configuration, protect secrets, apply database migrations safely, create a container image, run continuous checks, deploy to one environment, monitor rollout, and practice rollback and disaster recovery.

Learn Docker before Kubernetes. Use Kubernetes only when its workload, networking, storage, configuration, and operational costs solve an actual deployment problem.

### Stage 11: Architecture and System Evolution

Learn modular monoliths, service boundaries, synchronous and asynchronous communication, consistency tradeoffs, schema and API evolution, data ownership, load balancing, replication, partitioning, multi-tenancy, regional failure, and cost-aware design.

Do not begin with microservices. Extract a service only when ownership, scaling, isolation, deployment, or reliability evidence justifies the additional network and operational boundaries.

## Language implementation tracks

The curriculum provides these separate specializations:

- **[Node.js and TypeScript Backend](../learn-to-nodejs-backend/README.md):** Node runtime behavior, HTTP servers, framework selection, validation, PostgreSQL, jobs, tests, security, and deployment.
- **[Python Backend](../learn-to-python-backend/README.md):** ASGI, FastAPI for the API-first track, optional Django full-stack branch, PostgreSQL, background work, tests, security, and deployment.
- **[Go Backend](../learn-to-go-backend/README.md):** Standard-library HTTP foundations, focused routing and middleware, PostgreSQL, concurrency, background work, tests, security, and deployment.
- **[Java and Spring Backend](../learn-to-java-spring-backend/README.md):** Spring Boot, Spring MVC, validation, persistence, transactions, security, messaging, tests, JVM operations, and deployment.
- **[Rust Backend](../learn-to-rust-backend/README.md):** Tokio, HTTP layers, Axum, Serde validation, PostgreSQL, concurrency, tests, security, and deployment.

These tracks share outcomes but should not be copies with renamed syntax. Their module counts must follow the real boundaries and responsibilities of each ecosystem.

## Project milestones

Progress should be demonstrated through several projects instead of one final assessment:

1. Build a small server with a health route, structured configuration, request logging, graceful shutdown, and an automated HTTP test.
2. Build a versioned CRUD API with runtime validation, stable errors, PostgreSQL migrations, transactions, pagination, and integration tests.
3. Add accounts, secure sessions or tokens, resource ownership, roles, rate limits, audit events, and tested unauthorized paths.
4. Add one external service and one background job with timeouts, retries, idempotency, failure status, and recovery.
5. Add metrics and traces, run a load test, diagnose one slow database query, and define useful alerts.
6. Containerize and deploy the service with least privilege, health checks, safe migrations, a monitored rollout, backup restoration, and rollback.

There is no miscellaneous stage and no final assessment.

## Accuracy anchors for future modules

Future modules should be checked against current specifications and primary documentation:

- [RFC 9110: HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110)
- [OpenAPI Specification](https://spec.openapis.org/oas/)
- [OWASP API Security Project](https://owasp.org/www-project-api-security/)
- [RFC 9700: OAuth 2.0 Security Best Current Practice](https://www.rfc-editor.org/info/rfc9700/)
- [PostgreSQL documentation](https://www.postgresql.org/docs/current/)
- [OpenTelemetry documentation](https://opentelemetry.io/docs/)
- [Docker documentation](https://docs.docker.com/get-started/)
- [Kubernetes concepts](https://kubernetes.io/docs/concepts/)
- [Node.js learning documentation](https://nodejs.org/en/learn)
- [FastAPI tutorial](https://fastapi.tiangolo.com/tutorial/)
- [Spring Boot web documentation](https://docs.spring.io/spring-boot/reference/web/index.html)
- [Go net/http package](https://pkg.go.dev/net/http)
- [Tokio documentation](https://tokio.rs/tokio/tutorial)
- [Axum documentation](https://docs.rs/axum/latest/axum/)
