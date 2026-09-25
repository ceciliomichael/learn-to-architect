# Module 18: Testing and Testable Design

## Outcome

Write unit and integration tests, test success and failure paths, and structure logic so tests are deterministic and useful.

## Why this matters

Manual testing helps exploration but does not scale as regression protection. Automated tests record expected behavior and make repeated verification inexpensive.

## Programming concept

A test supplies controlled inputs, observes behavior, and checks expectations. Determinism means the same controlled setup gives the same relevant result. Testability improves when domain logic is separated from clocks, networks, files, and other external systems.

## Rust model

#[test] functions run under cargo test. assert, assert_eq, and assert_ne express expectations. Unit tests often live beside implementation under cfg(test). Integration tests live under tests/ and use the public library API like an outside consumer.

## Local Cargo example

Create cargo new calculator --lib --edition 2024 and put the example in src/lib.rs.

~~~rust
pub fn divide(total: i32, parts: i32) -> Result<i32, String> {
    if parts == 0 {
        return Err(String::from("parts cannot be zero"));
    }
    Ok(total / parts)
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn divides_evenly() {
        assert_eq!(divide(12, 3), Ok(4));
    }

    #[test]
    fn rejects_zero_parts() {
        assert!(divide(12, 0).is_err());
    }
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- Tests call ordinary functions with controlled values.
- Success and failure are both part of the contract.
- cfg(test) includes the test module during test builds.
- This pure function needs no external setup.
- An integration test under tests/ can exercise the same public API.

## Deliberate mistake

~~~rust
#[test]
fn weak_test() {
    let result = 2 + 2;
    println!("result is {result}");
}
~~~

This runs but asserts nothing. Printing is not a verification condition, so the test passes regardless of the intended expectation.

Corrected direction:

~~~rust
#[test]
fn addition_is_four() {
    let result = 2 + 2;
    assert_eq!(result, 4);
}
~~~

## Mental model

- Tests are executable expectations, not complete proofs.
- Test observable behavior and meaningful boundaries.
- A useful failing test explains a regression.
- Separate deterministic logic from external effects.
- Test errors and edge cases, not only happy paths.

## Common mistakes

- Tests with no assertions.
- Testing private implementation details unnecessarily.
- Calling real internet services from ordinary unit tests.
- Shared mutable global test state.
- Chasing coverage numbers instead of behavior.

## Transfer to other languages

Testing frameworks vary, but controlled inputs, observable outcomes, determinism, and useful failures transfer directly.

## Guided practice

1. Add a second success case.
2. Create a tests/public_api.rs integration test.
3. Test an error path.
4. Refactor a print-heavy calculation so its logic returns a value that can be asserted.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- write and run unit tests;
- explain unit versus integration tests;
- test failure behavior;
- identify an external dependency that should be separated from domain logic.

## Next

Continue to [Module 19](../19-generics-and-reusable-algorithms/README.md).
