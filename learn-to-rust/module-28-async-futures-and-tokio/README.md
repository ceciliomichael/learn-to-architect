# Module 28: Async Functions, Futures, and Tokio

An `async fn` returns a future. A future describes work that progresses when an executor polls it. Creating a future does not by itself run the whole operation. `.await` pauses this task until the awaited value is ready and lets the runtime work on other tasks.

The standard library defines futures, but an application needs a runtime for scheduling, timers, and async I/O. Create a Cargo project and add Tokio:

```text
cargo add tokio --features rt-multi-thread,macros,time
```

```rust
use std::time::Duration;

#[tokio::main]
async fn main() {
    let result = tokio::time::timeout(Duration::from_secs(1), async { 42 }).await;
    println!("{result:?}");
}
```

`tokio::spawn` returns a `JoinHandle`. Keep and await it when completion matters. Dropping the handle detaches the task, so the caller no longer observes its result. Runtime shutdown cancels unfinished tasks.

Cancellation happens at `.await` points. A future that is abandoned may have completed only part of its work, so design operations to remain valid when interrupted. Use timeouts around external work. Use `spawn_blocking` for short blocking operations that cannot become async, and limit their number.

Async helps programs wait for many I/O operations efficiently. It does not automatically make CPU-heavy work faster.

Continue to [Module 29](../module-29-networking-and-http-boundaries/README.md).
