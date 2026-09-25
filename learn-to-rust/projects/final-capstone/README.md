# Final Capstone: Production-Style Rust Application

## Purpose

This capstone is where the course stops telling you exactly what to type.

You now design and build a substantial Rust application using the ideas accumulated across the course.

The goal is not maximum feature count.

The goal is to demonstrate that you can:

- turn requirements into a design;
- choose ownership deliberately;
- separate policy from mechanisms;
- use external crates responsibly;
- model errors and invalid states;
- test behavior;
- manage files or network boundaries safely;
- use concurrency only when justified;
- make the system observable;
- review dependencies;
- build and package a release artifact;
- explain architectural tradeoffs.

## Recommended capstone

Build a local-first **Job Monitor and History CLI**.

The application manages named endpoint checks and stores historical results locally.

It should let an operator:

- add an endpoint;
- list endpoints;
- remove or disable an endpoint;
- run one endpoint check;
- run all enabled checks with bounded concurrency;
- inspect recent history;
- show summary statistics;
- configure timeout and concurrency limits;
- export a report;
- display version information.

The application is intentionally similar to real operational tooling while remaining small enough to build without a web framework or database server.

You may choose another domain if it satisfies the same engineering requirements.

## Why this project works as a capstone

It requires:

- CLI design;
- domain types;
- Option and Result;
- collections;
- modules/crates;
- serialization;
- file persistence;
- external crates;
- HTTP;
- async;
- bounded concurrency;
- observability;
- testing;
- architecture;
- dependency review;
- release engineering.

It does not require inventing a large distributed system.

## Required project structure

Use either:

- one well-structured Cargo package; or
- a small workspace when the crate boundaries are justified.

A reasonable workspace is:

~~~text
job-monitor/
  Cargo.toml
  Cargo.lock
  crates/
    domain/
    storage-json/
    app/
  docs/
  tests/
~~~

A simpler package is also acceptable if it remains clear.

Do not create crates only because the capstone description shows them.

## Architectural target

Conceptually:

~~~text
CLI
 |
 v
application orchestration
 |          \
 |           \--> diagnostics
 v
domain
 ^
 |
storage adapter

application
 |
 v
HTTP adapter
 |
 v
network
~~~

The domain should not need to know about:

- Clap;
- reqwest;
- terminal formatting;
- JSON parser details;
- tracing subscriber setup.

Adapters translate external representations into domain/application values.

## Core domain model

Design your own types, but a possible model is:

~~~text
EndpointId
Endpoint
CheckConfig
CheckOutcome
CheckRecord
History
Summary
~~~

Use newtypes where a raw primitive would blur important meaning.

Examples:

~~~text
EndpointId
TimeoutSeconds
ConcurrencyLimit
~~~

Do not wrap every primitive automatically.

Create a newtype when it strengthens the domain or prevents accidental interchange.

## Endpoint rules

At minimum:

- endpoint name cannot be empty;
- URL must be accepted only after your HTTP/URL parsing boundary validates it;
- timeout must be positive and bounded by your chosen application policy;
- concurrency limit must be nonzero and bounded;
- IDs must be unique;
- disabled endpoints are not included in run-all by default.

Document the exact rules.

## CLI

Use a maintained CLI crate already introduced in the course.

A possible interface:

~~~text
job-monitor endpoint add NAME URL
job-monitor endpoint list
job-monitor endpoint remove ID
job-monitor endpoint disable ID
job-monitor endpoint enable ID

job-monitor check ID
job-monitor check-all

job-monitor history ID
job-monitor summary

job-monitor export PATH
job-monitor --version
~~~

Your exact syntax may differ.

Requirements:

- useful help text;
- invalid syntax handled by the parser;
- domain errors reported clearly;
- diagnostics sent separately from normal output;
- meaningful process exit status.

## Configuration

Support a documented precedence.

For example:

~~~text
CLI option
  >
environment variable
  >
configuration file
  >
built-in default
~~~

Only implement sources you genuinely need.

Do not add four configuration systems just because the course mentions them.

At minimum, configure:

- data file path;
- request timeout;
- maximum concurrency.

## Persistence

Use a versioned local format.

Example conceptual shape:

~~~json
{
  "format_version": 1,
  "endpoints": [],
  "history": []
}
~~~

Requirements:

- malformed data returns a controlled error;
- unsupported format version is rejected deliberately;
- loaded domain values are validated after deserialization;
- missing file follows a documented first-run policy;
- saving does not casually destroy the last valid state before replacement data is ready;
- file path is configurable;
- tests use isolated temporary paths.

Do not claim crash-safe or atomic persistence without understanding and documenting the platform guarantees you actually use.

## History growth

History cannot grow forever without a policy.

Choose and document one:

- keep last N records per endpoint;
- keep records newer than a retention period;
- cap total records;
- another bounded policy.

Implement the policy in domain/application logic that can be tested without real HTTP.

## HTTP checking

Use a maintained HTTP client.

Requirements:

- one reusable client;
- TLS verification remains enabled;
- explicit timeout;
- bounded concurrency;
- failures represented as data, not process panics;
- distinguish at least:
  - healthy response;
  - non-success HTTP status;
  - timeout;
  - transport failure.

If response bodies are not needed, do not download and store them unnecessarily.

If you inspect bodies, enforce a deliberate maximum.

## URL trust boundary

For this local operator-controlled tool, endpoint URLs come from the operator.

Document that trust assumption.

If you later expose this functionality through a server where arbitrary remote users choose URLs, that becomes an SSRF/network-policy boundary and requires a different security design.

The capstone should recognize that architecture changes when the trust model changes.

## Bounded concurrency

The check-all operation must not launch unlimited external work.

Use an explicit limit.

Possible mechanisms include:

- semaphore;
- bounded task set;
- worker queue.

Document:

- where the bound is enforced;
- what owns the tasks;
- how completion is awaited;
- what happens when one task fails;
- how the program shuts down.

Do not use Arc Mutex shared state unless the design genuinely needs it.

Prefer returning per-task results and combining them after completion when possible.

## Cancellation

The application should remain valid if a task is cancelled or times out.

Ask:

- Was any history record partially created?
- Is persistence performed only after a complete outcome exists?
- Can one timed-out check prevent others from finishing?
- Are task handles accounted for?

You do not need a complex cancellation framework.

You do need to reason about incomplete async work.

## Errors

Design error boundaries.

Possible categories:

~~~text
ConfigError
StorageError
DomainError
CheckError
ApplicationError
~~~

Do not create these merely to satisfy the list.

Use structured error types where callers need categories.

Add context at boundaries.

Avoid:

~~~text
unwrap
expect
panic
~~~

for ordinary:

- user input;
- malformed files;
- missing files;
- network failure;
- timeout;
- HTTP error status.

Panic remains appropriate only for violated internal invariants or truly unrecoverable assumptions you can justify.

## Observability

Use structured tracing.

Include useful fields such as:

- endpoint ID;
- endpoint name when non-sensitive;
- operation;
- outcome category;
- elapsed time;
- request/check identifier if you add one.

Do not log:

- credentials;
- authorization headers;
- secret query parameters;
- entire sensitive payloads.

The normal CLI output should remain useful without reading diagnostic logs.

## Testing strategy

The final capstone must have more than happy-path unit tests.

### Domain unit tests

Test:

- endpoint validation;
- unique IDs;
- enable/disable behavior;
- retention policy;
- summary calculation;
- configuration resolution.

### Serialization tests

Test:

- round trip;
- malformed JSON;
- unsupported format version;
- invalid domain data after successful JSON parsing.

### Application tests

Test behavior with controlled adapters or values.

Avoid requiring public internet access for every test.

### HTTP classification tests

Separate response/outcome classification from real network calls where possible.

If you use a local test server dependency, review it like any other dependency.

### CLI tests

At minimum verify important parser behavior and one end-to-end harmless command path.

### Regression tests

When you find a bug during development:

1. reproduce it;
2. add a failing test when practical;
3. fix it;
4. keep the test.

## Dependency policy

Create:

~~~text
docs/DEPENDENCIES.md
~~~

For every direct external dependency record:

- purpose;
- features enabled;
- why standard library is insufficient;
- important transitive impact;
- license information you have verified;
- security/update process;
- removal or replacement considerations.

Run:

~~~text
cargo tree
~~~

Understand why every direct dependency exists.

## Architecture document

Create:

~~~text
docs/ARCHITECTURE.md
~~~

Include:

### System purpose

One paragraph.

### Components

What each module/crate owns.

### Dependency direction

Plain-text diagram.

### State ownership

Who owns:

- configuration;
- endpoints;
- history;
- HTTP client;
- async tasks.

### External boundaries

- filesystem;
- environment;
- terminal;
- network.

### Error flow

Where errors originate, how they are translated, and where they are reported.

### Concurrency

Why async/concurrency is used and how it is bounded.

### Security assumptions

Especially URL trust and local file trust.

### Rejected alternatives

Document at least two designs you considered but did not choose.

Examples:

- database instead of JSON;
- global Arc Mutex state;
- one OS thread per endpoint;
- one crate per layer.

Explain why you rejected them.

## Performance document

Create:

~~~text
docs/PERFORMANCE.md
~~~

Do not invent impressive numbers.

Define at least one meaningful question, such as:

~~~text
How does check-all behave with 100 configured endpoints and concurrency limit 10?
~~~

Record:

- workload;
- release build;
- baseline;
- bottleneck evidence;
- result.

A valid conclusion can be:

~~~text
No optimization is currently justified.
~~~

## Security document

Create:

~~~text
docs/SECURITY.md
~~~

Cover:

- dependency update process;
- advisory scanning process;
- secrets policy;
- URL trust model;
- file permissions assumptions;
- logging redaction;
- release credentials;
- unsafe/FFI statement.

If you use no unsafe code, say so.

Do not add unsafe code merely to have something to document.

## SBOM

Create an SBOM plan and, if your selected current tooling supports it, generate an SBOM for the release artifact.

Record:

- format;
- artifact/version;
- generation command/tool;
- where it is stored;
- how it would be used during a vulnerability response.

Do not fabricate component information manually when tooling can derive it.

## Release requirements

Your capstone must have a repeatable release procedure.

At minimum:

~~~text
cargo fmt --check
cargo clippy --workspace --all-targets --all-features
cargo test --workspace --all-features
cargo build --workspace --release --locked
~~~

Adjust workspace/all-features flags to match your actual project structure and supported matrix.

Then:

- smoke-test the built binary directly;
- record version/source revision;
- package required files;
- create checksums;
- include SBOM if required/generated;
- prepare release notes;
- document rollback.

Do not publish anything from the course unless you intentionally want to.

## Version command

The final binary should identify itself.

For example:

~~~text
job-monitor --version
~~~

A user should be able to tell which build is running.

## Git discipline

Use version control during the capstone.

A practical workflow:

1. create a repository if needed;
2. commit a clean starting point;
3. make small coherent changes;
4. inspect diffs;
5. write useful commit messages;
6. use branches when they help isolate larger work.

Git is not a Rust requirement.

It is a normal professional development tool.

## Milestone 1: Domain only

Build:

- Endpoint;
- IDs;
- configuration values;
- CheckOutcome;
- history;
- retention;
- summaries.

No HTTP yet.

No CLI yet.

Test domain behavior.

## Milestone 2: Storage

Add:

- versioned JSON representation;
- adapter;
- validation;
- round-trip tests;
- invalid-data tests.

Keep domain independent from JSON details when practical.

## Milestone 3: CLI

Add typed CLI parsing.

Wire commands to application behavior.

Do not implement check-all concurrency yet.

## Milestone 4: One HTTP check

Add:

- reusable client;
- one endpoint check;
- timeout;
- outcome classification;
- tracing.

Persist one completed outcome.

## Milestone 5: Bounded check-all

Add:

- concurrency limit;
- complete result accounting;
- history update;
- final summary.

Test the aggregation logic independently from internet access.

## Milestone 6: Hardening

Add:

- configuration precedence;
- retention;
- structured error categories where useful;
- logging review;
- file size/resource limits;
- help/version behavior;
- dependency review.

## Milestone 7: Performance and security review

Write:

- PERFORMANCE.md;
- SECURITY.md;
- DEPENDENCIES.md.

Run the project under a representative local workload.

Remove dependencies you do not need.

## Milestone 8: Release

Run the release gate.

Build the final artifact.

Smoke-test it directly.

Package it.

Write release notes and rollback procedure.

## Definition of done

The capstone is complete when:

### Functionality

- endpoint CRUD or equivalent management works;
- persistent state loads and saves;
- single check works;
- bounded check-all works;
- history works;
- summary works;
- version/help work.

### Reliability

- external failures do not panic the whole process;
- invalid files are handled;
- unsupported schema versions are handled;
- concurrency is bounded;
- every launched task is accounted for;
- save errors are reported.

### Code quality

- formatting passes;
- Clippy passes or every allowed lint has a documented reason;
- tests pass;
- ownership is understandable;
- unnecessary clone calls have been reviewed;
- no broad unsafe code has been introduced.

### Architecture

- domain responsibilities are clear;
- external boundaries are isolated reasonably;
- global mutable state is avoided;
- dependency direction is documented;
- abstractions have real purposes.

### Security

- TLS verification remains enabled;
- secrets are not logged or committed;
- response/resource limits exist where needed;
- URL trust assumptions are documented;
- dependencies are reviewed.

### Delivery

- release build uses the lock file;
- artifact is smoke-tested;
- version is identifiable;
- release procedure is documented;
- rollback is considered;
- SBOM plan exists.

## Final self-review

Before calling the course complete, answer these without looking up definitions:

1. What is ownership?
2. What is borrowing?
3. Why are lifetimes relationships rather than timers?
4. When would you use Option versus Result?
5. When is a trait useful?
6. When is a trait object useful?
7. Why is Arc not the same as a mutex?
8. Why is async not a speed switch?
9. What is backpressure?
10. Why do external inputs remain untrusted after parsing?
11. What is a dependency trust boundary?
12. Why measure before optimizing?
13. What makes a public API hard to change?
14. What is dependency direction?
15. What separates a build from a release?
16. How would you begin learning an unfamiliar language tomorrow?

If you can explain those in your own words and build the capstone without following a complete solution, the course has accomplished its larger goal.

## What comes after

Do not immediately start another giant tutorial.

Choose work that forces you to apply the skills:

- contribute a small fix to a Rust project;
- build a tool you actually use;
- read a crate's implementation;
- learn one specialized Rust domain;
- rebuild a familiar project in another language.

The goal was never to finish a list of Rust topics.

The goal was to become someone who can reason about software and keep learning.
