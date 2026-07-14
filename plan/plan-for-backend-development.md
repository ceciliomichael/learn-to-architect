# Plan for the Backend Engineering Learning Path

## Goal

Create a beginner-to-advanced backend path that begins with real repository courses, lets the learner choose one primary server language, and teaches shared server responsibilities without forcing unrelated frontend frameworks or several backend languages.

## Curriculum decisions

- Git begins early, while advanced recovery and maintenance return during larger projects.
- Learners choose TypeScript, Python, Go, Java, or Rust as one primary branch.
- C remains a later systems option rather than the recommended first application-server language.
- SQL is required and appears before each language's database integration boundary.
- HTTP semantics are taught before framework conventions.
- Runtime validation is required at every network and storage boundary.
- Relational SQL and transactions are taught before ORM convenience.
- Authentication and authorization remain separate concepts.
- Background work includes idempotency, status, failure, and recovery.
- Security, testing, observability, and operations appear throughout the path and later receive dedicated treatment.
- A modular monolith comes before microservices.
- Docker comes before Kubernetes.
- One deployment environment is learned deeply before comparing cloud providers.
- REST and OpenAPI form the first API track. GraphQL, gRPC, WebSockets, and server-sent events remain problem-driven options.
- Future module counts follow the real boundaries of each ecosystem and will not be copied from another course.

## Existing course audit

- [x] Confirm Git provides beginner collaboration plus advanced recovery, automation, and release skills
- [x] Confirm SQL covers modeling, transactions, migrations, concurrency, PostgreSQL, access control, and tuning
- [x] Confirm TypeScript covers runtime validation, async request boundaries, installed types, and testing
- [x] Confirm Python's database boundary begins at Module 33
- [x] Confirm Go's HTTP server and database boundaries occur at Modules 28 and 29
- [x] Confirm Java's HTTP client and JDBC boundaries occur at Modules 30 and 31
- [x] Confirm Rust covers Tokio and HTTP boundaries but not a complete application-server specialization
- [x] Identify the missing backend foundation and implementation tracks

## Path document

- [x] Define safe beginner ordering for every language branch
- [x] Keep TypeScript backend independent from React and Next.js
- [x] Define eleven shared backend stages
- [x] Define five language-specific implementation tracks
- [x] Explain where C fits without presenting it as the default beginner branch
- [x] Define project milestones instead of a final assessment
- [x] Add current primary specification and documentation anchors
- [x] Add the path to repository navigation

## Completed curriculum roadmap

The shared areas are implemented in Backend Foundations and reinforced inside each applicable language track. The five implementation tracks remain separate courses so learners never need to switch languages during one backend project.

- [x] Implement Server, Network, and HTTP Foundations
- [x] Implement Node.js and TypeScript Backend
- [x] Implement Python Backend
- [x] Implement Go Backend
- [x] Implement Java and Spring Backend
- [x] Implement Rust Backend
- [x] Implement API Contracts and Runtime Validation
- [x] Implement Relational Persistence and Transactions
- [x] Implement Identity, Sessions, and Authorization
- [x] Implement External Services, Caching, and Background Work
- [x] Implement Backend Testing, Concurrency, and Reliability
- [x] Implement Backend Security Engineering
- [x] Implement Observability and Performance
- [x] Implement Packaging, Deployment, and Operations
- [x] Implement Backend Architecture and System Evolution

Every module keeps the repository's lesson, exercise, quiz, exercise answer, and quiz answer structure. No miscellaneous module or final assessment is included.
