# Module 27: Logging, Diagnostics, and Debugging

## Outcome

Diagnose failures systematically, distinguish user output from observability, use structured tracing, read backtraces, and produce reproducible bug reports.

## Why this matters

Bugs do not become easier because a program is larger. Production systems need enough evidence to answer what happened, where, under which inputs, and with which request or operation context.

## Programming concept

Observability is the evidence a system exposes about its behavior. Logs are event records, traces connect related work, metrics summarize numeric behavior, and debugging is the process of forming and testing hypotheses from evidence. Reproduction narrows uncertainty.

## Rust model

dbg! is a source-level development aid that prints expression values and locations to stderr. RUST_BACKTRACE can expose stack backtraces for panics. The tracing ecosystem supports structured events and spans. A subscriber decides how those events are collected or formatted.

## Local Cargo example

Create cargo new diagnostics --edition 2024, run cargo add tracing and cargo add tracing-subscriber, then replace src/main.rs.

~~~rust
use tracing::{info, instrument, warn};

#[instrument]
fn process_item(id: u32) -> Result<(), String> {
    if id == 0 {
        warn!("invalid item id");
        return Err(String::from("id must be nonzero"));
    }

    info!(item_id = id, "processing item");
    Ok(())
}

fn main() {
    tracing_subscriber::fmt()
        .with_target(false)
        .init();

    for id in [1, 0] {
        if let Err(error) = process_item(id) {
            eprintln!("could not process item: {error}");
        }
    }
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- A subscriber is initialized once near the application boundary.
- instrument creates a span around the function call and can capture arguments.
- info and warn record structured events rather than concatenating every fact into one string.
- The lower function returns the error while the boundary decides the user-facing message.
- Logs should contain useful context without secrets or excessive payloads.

## Deliberate mistake

~~~rust
fn authenticate(password: &str) {
    println!("login attempt with password={password}");
}
~~~

Diagnostics can become persistent data. Logging credentials, access tokens, private keys, or sensitive personal information creates a new security exposure.

Corrected direction:

~~~rust
fn authenticate(account_id: &str) {
    tracing::info!(account_id, "login attempt");
}
~~~

## Mental model

- Start debugging by reproducing and reducing the problem.
- Read the first relevant compiler/runtime error before guessing.
- Record stable identifiers and operation context, not secrets.
- Log at the layer that has meaningful context and avoid duplicating the same error at every layer.
- Structured fields are easier to filter and aggregate than hand-built text.

## Common mistakes

- Logging secrets.
- Using logging instead of returning errors.
- Printing the same failure at every stack layer.
- Adding so much debug output that signal disappears.
- Fixing symptoms without creating a reproduction or test.

## Transfer to other languages

Logging frameworks differ, but evidence-driven debugging, structured context, correlation, redaction, and reproducible reports are universal engineering skills.

## Guided practice

1. Use dbg! on a local expression and note it writes to stderr.
2. Enable a backtrace for an intentional panic in a disposable program.
3. Add a tracing field rather than interpolating it into message text.
4. Write reproduction steps for one deliberate bug.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- separate program output from diagnostics;
- initialize and emit structured tracing events;
- avoid sensitive logging;
- describe a reproduce-reduce-hypothesize-test debugging loop.

## Next

Continue to [Checkpoint Project D](../projects/project-d-persistent-cli/README.md).
