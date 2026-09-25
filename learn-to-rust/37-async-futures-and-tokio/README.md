# Module 37: Async Functions, Futures, and Tokio

## Outcome

Explain the Future model, use async and await with Tokio, add timeouts and task boundaries, understand cancellation, and keep blocking or CPU-heavy work from accidentally stalling async execution.

## Why this matters

Threads are useful, but a program waiting on thousands of sockets does not necessarily need thousands of operating-system threads. Asynchronous programming lets a smaller set of runtime threads make progress on many tasks that frequently wait for I/O.

## Programming concept

A future represents work that may not be complete yet. An executor repeatedly polls futures that can make progress. Cooperative scheduling means a task yields at await points instead of being forcibly interrupted at arbitrary instructions. Cancellation means work may be abandoned before every intended side effect has happened.

## Rust model

The standard library defines the Future trait, while an async runtime supplies scheduling, timers, and async I/O. Tokio is a widely used runtime. async fn returns a future. Await waits for that future while allowing the runtime to schedule other ready work. tokio::spawn creates an independently scheduled task. Timeouts and explicit cancellation should be part of external-I/O design rather than afterthoughts.

## Local Cargo example

Create cargo new async_runtime --edition 2024. Then run cargo add tokio --features rt-multi-thread,macros,time,sync.

~~~rust
use std::time::Duration;
use tokio::time::{sleep, timeout};

async fn simulated_lookup(id: u32) -> u32 {
    sleep(Duration::from_millis(50)).await;
    id * 10
}

#[tokio::main]
async fn main() {
    match timeout(Duration::from_secs(1), simulated_lookup(7)).await {
        Ok(value) => println!("value: {value}"),
        Err(_) => eprintln!("lookup timed out"),
    }
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- Calling simulated_lookup creates a future whose work progresses when it is awaited or otherwise polled.
- Tokio's sleep yields rather than blocking the runtime thread for the duration.
- timeout wraps another future and returns an error if the deadline wins.
- The tokio::main macro starts a runtime and runs the async main future.
- The timeout only limits this operation. It does not prove every nested external call has the right timeout or cancellation behavior.

## Deliberate mistake

~~~rust
use std::{thread, time::Duration};

async fn bad_wait() {
    thread::sleep(Duration::from_secs(5));
}
~~~

std::thread::sleep blocks the runtime worker thread executing this future. Other tasks assigned to that worker cannot make progress during the sleep. Async code must distinguish cooperative async waiting from blocking work.

Corrected direction:

~~~rust
use std::time::Duration;

async fn good_wait() {
    tokio::time::sleep(Duration::from_secs(5)).await;
}
~~~

## Mental model

- Creating a future is not the same as completing its work.
- Await is a suspension point where other tasks may run.
- Async is primarily about efficient waiting and concurrency, not automatically making CPU work faster.
- External operations need timeout and cancellation design.
- A future can be dropped before completion, so partial side effects must leave valid state.
- Use spawn_blocking for unavoidable blocking operations, and bound how much blocking work you create.
- Keep ownership across await points simple; avoid holding locks or borrowed guards across await unless the API and design explicitly make that safe.

## Common mistakes

- Using async because it sounds faster for CPU-heavy work.
- Calling blocking filesystem, sleep, or legacy APIs on runtime worker threads without a strategy.
- Spawning tasks and ignoring their JoinHandle when completion matters.
- Holding a std::sync::Mutex guard across await.
- Assuming timeout automatically rolls back side effects already performed.
- Creating unbounded numbers of tasks for unbounded input.

## Transfer to other languages

JavaScript promises, Python asyncio, C# tasks, Kotlin coroutines, Java virtual-thread or reactive models, and other systems solve overlapping waiting/scheduling problems differently. The transferable concepts are suspension, scheduling, cancellation, timeouts, bounded concurrency, and blocking boundaries.

## Guided practice

1. Call two independent async functions with tokio::join! and compare the structure with sequential awaits.
2. Wrap a simulated slow operation in timeout.
3. Spawn one task, retain its JoinHandle, and await the result.
4. Use spawn_blocking for a deliberately blocking practice closure and explain why it belongs outside the async worker path.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- explain future, executor, async, and await without saying async means a new thread;
- use a Tokio timer and timeout;
- distinguish blocking work from async waiting;
- state what happens when completion matters but a spawned task handle is ignored;
- describe cancellation as a normal control-flow possibility.

## Next

Continue to [Module 38](../38-networking-and-http-boundaries/README.md).
