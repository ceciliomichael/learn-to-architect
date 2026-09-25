# Module 38: Networking and HTTP Boundaries

## Outcome

Understand sockets and HTTP at a practical systems level, make bounded HTTPS requests with a maintained client, handle status and body limits, and design retries around partial failure and idempotency.

## Why this matters

Networks are external systems with latency, disconnection, DNS failure, TLS negotiation, remote overload, malformed responses, and partial completion. A successful local build says nothing about whether a remote operation will succeed or whether retrying it is safe.

## Programming concept

A network protocol defines how independent machines exchange messages. HTTP uses requests and responses over a transport stack. Distributed operations can fail before, during, or after the remote side acts, so callers may not always know whether an operation took effect. Idempotency describes whether repeating an operation has the same intended effect as performing it once.

## Rust model

The standard library provides TCP and UDP primitives. Production HTTP and TLS involve enough protocol and security detail that applications should normally use a maintained client. Reqwest provides an HTTP client, while Tokio drives its async I/O. Client-wide and operation-specific timeouts, status validation, bounded body processing, and TLS verification remain application responsibilities.

## Local Cargo example

Create cargo new http_client --edition 2024. Run cargo add tokio --features rt-multi-thread,macros and cargo add reqwest --features rustls-tls.

~~~rust
use std::time::Duration;

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let client = reqwest::Client::builder()
        .timeout(Duration::from_secs(5))
        .build()?;

    let response = client
        .get("https://example.com/")
        .send()
        .await?
        .error_for_status()?;

    let status = response.status();
    let body = response.text().await?;

    println!("status: {status}");
    println!("body bytes: {}", body.len());
    Ok(())
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- A reusable Client holds connection-pool and protocol configuration instead of creating ad hoc clients for every request.
- The client timeout prevents this demonstration request from waiting indefinitely.
- send can fail before an HTTP response exists because DNS, connection, TLS, or transport can fail.
- error_for_status converts error HTTP status codes into a failure path instead of treating every response as application success.
- text buffers the complete body. That is acceptable for known-small demonstration content, but untrusted large responses need explicit streaming and size limits.

## Deliberate mistake

~~~rust
async fn fetch() {
    let body = reqwest::get("https://example.com/")
        .await
        .unwrap()
        .text()
        .await
        .unwrap();

    println!("{}", body.len());
}
~~~

This turns normal network failures into panics, creates an ad hoc request path without an explicit application timeout policy, ignores HTTP status semantics, and buffers the full body without stating a size assumption.

Corrected direction:

~~~rust
use std::time::Duration;

async fn fetch(client: &reqwest::Client) -> Result<reqwest::Response, reqwest::Error> {
    client
        .get("https://example.com/")
        .timeout(Duration::from_secs(5))
        .send()
        .await?
        .error_for_status()
}
~~~

## Mental model

- Network calls are fallible even when your input URL is correct.
- Separate transport failure, HTTP status failure, parse failure, and domain failure.
- Use timeouts at external boundaries.
- Do not disable TLS certificate verification to make a problem disappear.
- Retry only when the operation and failure mode make repetition acceptable; use bounded attempts and backoff rather than tight loops.
- Treat remote response size and content as untrusted.
- A server-provided Content-Length can help planning but is not by itself a complete enforcement mechanism for every response path.

## Common mistakes

- Using unwrap around DNS, connection, or HTTP failures.
- Retrying non-idempotent operations blindly.
- Retrying immediately and indefinitely during an outage.
- Disabling TLS verification.
- Buffering unlimited response bodies.
- Logging authorization headers or tokens.
- Allowing arbitrary user-supplied destinations in a server-side fetch feature without considering SSRF and network policy.

## Transfer to other languages

HTTP libraries differ, but DNS, transport, TLS, timeouts, retries, status codes, partial failure, body limits, and trust boundaries apply in every networked ecosystem.

## Guided practice

1. Reuse one Client for several requests rather than constructing one per call.
2. Request an endpoint that returns a non-success status and observe error_for_status.
3. Add a per-request timeout shorter than the client default.
4. Read Reqwest's response streaming API documentation and outline how you would enforce a maximum downloaded body size without trusting only Content-Length.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- describe HTTP request/response at a practical level;
- distinguish transport, status, parsing, and domain failure;
- configure a timeout;
- explain why retry safety depends on operation semantics;
- treat network destinations and response bodies as untrusted boundaries.

## Next

Continue to [Checkpoint Project E](../projects/project-e-concurrent-networked-app/README.md).
