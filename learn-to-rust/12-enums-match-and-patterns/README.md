# Module 12: Enums, Match, and Pattern Matching

## Outcome

Model a value that can be one of several meaningful variants, attach data to variants, and handle states exhaustively with patterns.

## Why this matters

Many domains contain mutually exclusive states: pending, running, completed, failed. Representing these as unrelated Booleans can accidentally allow impossible combinations. A sum type models exactly which alternatives exist.

## Programming concept

A sum type represents one value chosen from several alternatives. Pattern matching both identifies the alternative and can destructure its contained data. Exhaustiveness means every possible variant has a defined handling path.

## Rust model

Rust enums define variants, and each variant may carry different data. match requires exhaustive handling unless a catch-all pattern covers the remainder. if let and let else are concise tools when only one pattern is central, but match is often clearest when several states matter.

## Local Cargo example

~~~text
cargo new enums_and_match --edition 2024
cd enums_and_match
~~~

Replace src/main.rs:

~~~rust
enum JobState {
    Queued,
    Running { percent: u8 },
    Failed(String),
    Complete,
}

fn describe(state: &JobState) -> String {
    match state {
        JobState::Queued => String::from("queued"),
        JobState::Running { percent } => format!("running: {percent}%"),
        JobState::Failed(message) => format!("failed: {message}"),
        JobState::Complete => String::from("complete"),
    }
}

fn main() {
    let state = JobState::Running { percent: 40 };
    println!("{}", describe(&state));
}
~~~

Run cargo check, cargo run, and cargo fmt.

Expected output:

~~~text
running: 40%
~~~


## Walkthrough

- JobState says a job has exactly one represented state at a time.
- Running carries a named percent field; Failed carries an owned message.
- match borrows the enum and handles every variant.
- Patterns extract data such as percent or message.
- Adding a new variant later forces relevant exhaustive matches to be reconsidered.

## Deliberate mistake

~~~rust
enum Direction {
    North,
    South,
    East,
    West,
}

fn label(value: Direction) -> &'static str {
    match value {
        Direction::North => "N",
        Direction::South => "S",
    }
}
~~~

The match ignores East and West. Rust rejects the non-exhaustive match instead of silently leaving those states undefined.

Corrected version:

~~~rust
enum Direction {
    North,
    South,
    East,
    West,
}

fn label(value: Direction) -> &'static str {
    match value {
        Direction::North => "N",
        Direction::South => "S",
        Direction::East => "E",
        Direction::West => "W",
    }
}
~~~

## Mental model

- An enum value is one variant at a time.
- Put variant-specific data inside the variant that needs it.
- Exhaustive matches make state changes visible to the compiler.
- Use a catch-all only when the grouped states truly share behavior.
- Model valid states directly instead of maintaining combinations of unrelated flags.

## Common mistakes

- Using multiple Booleans for mutually exclusive states.
- Adding _ just to silence an exhaustiveness error.
- Putting fields on every state when only one variant needs them.
- Using if let when many variants need distinct handling.
- Treating enums as integer constants only; Rust variants can carry rich data.

## Transfer to other languages

Algebraic data types, tagged unions, discriminated unions, sealed hierarchies, and variants solve the same modeling problem in other languages. Exhaustive checking is particularly valuable when the domain evolves.

## Guided practice

1. Create an enum for traffic-light state.
2. Add data to one variant.
3. Write an exhaustive match.
4. Replace a one-interesting-case match with if let and explain whether it became clearer.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before reading the answers.

## Readiness check

- model mutually exclusive states with an enum;
- attach data to variants;
- destructure variants in patterns;
- explain the value of exhaustive matching.

## Next

Continue to [Module 13](../13-option-and-optional-values/README.md).
