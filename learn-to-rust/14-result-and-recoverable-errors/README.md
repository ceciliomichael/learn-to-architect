# Module 14: Recoverable Errors with Result

## Outcome

Represent success and failure with Result, propagate errors with ?, add useful context, and distinguish recoverable failures from violated invariants.

## Why this matters

Files can be missing, input can be malformed, requests can fail, and permissions can be denied. Many failures are expected possibilities that callers should be able to handle rather than process-ending surprises.

## Programming concept

A recoverable error is part of a function's possible outcome. Error propagation lets lower-level code report failure to a caller that has enough context to decide what to do. Good errors preserve useful cause without exposing secrets.

## Rust model

Result<T, E> is Ok(T) or Err(E). match handles both directly. The ? operator returns early on Err and unwraps Ok for continued computation, using compatible error conversion when available. panic is for broken invariants or situations the program cannot meaningfully continue from, not routine bad input.

## Local Cargo example

~~~text
cargo new result_errors --edition 2024
cd result_errors
~~~

Replace src/main.rs:

~~~rust
fn parse_positive(text: &str) -> Result<u32, String> {
    let value: u32 = text
        .trim()
        .parse()
        .map_err(|error| format!("not a valid unsigned integer: {error}"))?;

    if value == 0 {
        return Err(String::from("value must be greater than zero"));
    }

    Ok(value)
}

fn main() {
    for input in ["12", "0", "hello"] {
        match parse_positive(input) {
            Ok(value) => println!("{input:?} -> {value}"),
            Err(error) => println!("{input:?} -> error: {error}"),
        }
    }
}
~~~

Run cargo check, cargo run, and cargo fmt.



## Walkthrough

- The signature makes failure part of the contract.
- parse itself returns a parsing Result.
- map_err adds domain context while preserving a useful cause description.
- ? stops parse_positive early if parsing failed.
- Zero parses successfully but violates the function's domain rule, so it becomes a separate Err.
- main is the reporting boundary here and decides how to present errors.

## Deliberate mistake

~~~rust
fn parse_age(text: &str) -> u32 {
    text.parse().unwrap()
}

fn main() {
    println!("{}", parse_age("not-a-number"));
}
~~~

Invalid external input is an expected possibility. unwrap turns that ordinary failure into a panic, preventing the caller from choosing how to recover.

Corrected version:

~~~rust
fn parse_age(text: &str) -> Result<u32, String> {
    text.parse::<u32>()
        .map_err(|error| format!("invalid age: {error}"))
}

fn main() {
    match parse_age("not-a-number") {
        Ok(age) => println!("{age}"),
        Err(error) => println!("{error}"),
    }
}
~~~

## Mental model

- Result means success or a described failure.
- Return errors from lower layers; decide user-facing wording at an appropriate boundary.
- Use ? to propagate after you understand the equivalent match.
- Add context that explains what operation failed.
- Reserve panic for violated invariants or unrecoverable program assumptions, not normal user mistakes.

## Common mistakes

- Using unwrap to avoid designing error handling.
- Logging and returning the same error at every layer, creating duplicate noise.
- Erasing useful source context with a vague error.
- Putting secrets or raw credentials in errors.
- Using String errors forever in large libraries when structured categories would improve callers' decisions.

## Transfer to other languages

Exceptions, error codes, Either types, Result types, and rejected promises are different error models. The transferable skills are identifying failure boundaries, preserving context, separating recovery from reporting, and deciding which layer owns the response.

## Guided practice

1. Match a parse Result manually.
2. Rewrite the manual propagation using ?.
3. Create a function that returns a domain validation Err after successful parsing.
4. Add context to distinguish which field failed.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before reading the answers.

## Readiness check

- explain Ok and Err;
- use match and ? appropriately;
- distinguish parsing failure from domain validation failure;
- separate error creation, propagation, and final reporting;
- explain why routine invalid input should not panic.

## Next

Continue to [Checkpoint Project B](../projects/project-b-text-data-processor/README.md).
