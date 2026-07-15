# Module 29: Networking and HTTP Boundaries

TCP provides an ordered byte stream between two endpoints. It does not preserve message boundaries. An application protocol must define framing, maximum sizes, timeouts, and valid messages. Use `TcpListener` and `TcpStream` for learning or a protocol you control. Use a maintained HTTP library rather than writing HTTP or TLS yourself.

For an async HTTP client, add the current reqwest and Tokio releases:

```text
cargo add reqwest
cargo add tokio --features rt-multi-thread,macros
```

Create and reuse one `reqwest::Client` so its connection pool is reused. Build it with a total timeout because the library default should not be your application policy.

```rust
use std::time::Duration;

fn build_client() -> Result<reqwest::Client, reqwest::Error> {
    reqwest::Client::builder()
        .timeout(Duration::from_secs(10))
        .build()
}
```

Parse and validate URLs. Prefer HTTPS, restrict destinations when the caller controls the URL, and consider redirects part of that policy. Check the status with `error_for_status`, limit response bodies while reading them, and validate decoded data as untrusted input.

Retries are not automatically safe. A repeated request may perform an action twice. Retry only operations known to be idempotent, use a small budget and backoff, and honor the remote service's limits.

The Playground is unsuitable for reliable network exercises because sandbox network access can be restricted. Use a local Cargo project.

Continue to [Module 30](../30-command-line-configuration-and-logging/README.md).
