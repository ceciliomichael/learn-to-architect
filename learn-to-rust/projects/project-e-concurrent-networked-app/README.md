# Checkpoint Project E: Concurrent Networked Application

## Goal

Build a local asynchronous endpoint monitor that checks an operator-controlled list of HTTP or HTTPS URLs with bounded concurrency.

This checkpoint combines threads/concurrency reasoning, message/result modeling, synchronization choices, Tokio, and HTTP boundary design.

## Dependencies

Use Cargo to add only the capabilities you need. A reasonable baseline is:

~~~text
cargo add tokio --features rt-multi-thread,macros,time,sync
cargo add reqwest --features rustls-tls
cargo add serde --features derive
cargo add serde_json
cargo add tracing
cargo add tracing-subscriber
~~~

If you add more crates, update your dependency review.

## Input

Read a small local configuration file containing:

- endpoint name;
- URL;
- timeout seconds;
- enabled flag.

Validate configuration after deserialization.

For this course project, URLs are controlled by the person operating the local program. If the design were changed into a server that fetches arbitrary user-supplied URLs, that would create an SSRF/network-policy boundary requiring destination restrictions.

## Required behavior

- reuse one reqwest Client;
- process only enabled endpoints;
- bound in-flight checks, for example to four;
- apply a timeout;
- distinguish success, HTTP error status, timeout, and transport error;
- never panic because one endpoint failed;
- produce one final summary;
- emit structured diagnostic events without credentials or full sensitive payloads;
- wait for all launched checks before normal process exit.

## Response policy

Do not download unlimited response bodies.

If the monitor needs only availability and status, avoid consuming the full body. If you add body inspection, stream it and enforce an application maximum.

Do not disable certificate validation.

## Retry extension

Retries are optional. If implemented:

- retry only operations whose semantics are safe for your use case;
- use a small maximum attempt count;
- add a delay/backoff policy;
- do not turn a remote outage into an aggressive request loop;
- record final outcome and attempt count.

## Domain model

Prefer a result enum such as:

~~~rust
enum CheckOutcome {
    Healthy { status: u16, elapsed_ms: u128 },
    HttpError { status: u16 },
    Timeout,
    TransportError { message: String },
}
~~~

Adjust the exact model to your implementation.

## Tests

Do not make every test depend on the public internet.

Separate:

- configuration validation;
- outcome classification;
- summary aggregation;
- retry-decision logic;

from actual network I/O so those rules can be unit-tested deterministically.

One explicitly marked integration test may use a local test server if you choose a maintained testing approach.

## Quality gate

~~~text
cargo fmt --check
cargo clippy --all-targets --all-features
cargo test
cargo check
cargo tree
~~~

Explain why every direct dependency is present.

## Reflection

Compare three possible designs:

1. one operating-system thread per endpoint;
2. one async task per endpoint with a concurrency bound;
3. a small fixed worker system using message passing.

Explain what the workload is waiting for, where backpressure exists, and which design makes cancellation and resource limits easiest to reason about.

Continue to [Module 39](../../39-cargo-features-and-workspaces/README.md).
