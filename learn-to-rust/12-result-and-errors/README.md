# Module 12: Recoverable Errors with Result

## What you will learn

You will return useful failures, propagate them with `?`, and keep panic for broken invariants.

```rust
fn parse_quantity(text: &str) -> Result<u32, String> {
    let value: u32 = text
        .trim()
        .parse()
        .map_err(|error| format!("invalid quantity: {error}"))?;
    if value == 0 {
        return Err(String::from("quantity must be positive"));
    }
    Ok(value)
}
```

`Result<T, E>` is `Ok(T)` or `Err(E)`. Match it directly first. `?` returns an error early after applying an available conversion. It does not log or display the error.

Libraries should return typed errors. Commands decide user wording and exit status. Avoid exposing secrets or internal details. A custom enum makes expected failure categories explicit. After traits and lifetimes have been taught, larger libraries can implement the standard `Display` and `Error` traits and preserve source errors.

Panic is appropriate for an unrecoverable violated invariant, not invalid user input or a missing file.

## Check your understanding

You are ready when you can separate error creation, propagation, context, and final reporting.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
