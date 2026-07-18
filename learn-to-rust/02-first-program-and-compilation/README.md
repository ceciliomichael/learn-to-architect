# Module 02: Compile and Run Your First Program

## What you will learn

You will identify the entry function, statements, macro calls, and debug and release builds.

```rust
fn main() {
    // This result is intentionally stable for a later test.
    println!("Welcome to Rust");
    println!("{} + {} = {}", 2, 3, 2 + 3);
}
```

`fn main()` is the entry point of a binary crate. Braces create its block. Statements commonly end with semicolons. Rust also has value-producing expressions, taught gradually.

`println!` is a macro, shown by `!`. Its format string is fixed source text and later arguments fill placeholders. Debug formatting uses `{:?}` for values that implement `Debug`; use intentional user-facing formatting in real interfaces.

`cargo run` builds a debug artifact and runs it. `cargo build --release` enables optimizations and writes under `target/release`. Debug builds favor compilation speed and checks; release builds favor runtime performance. Test correctness in both when optimization-sensitive behavior matters.

Comments start with `//`. Explain constraints and reasons, not obvious syntax. Cargo rejects many warnings only when configured to, so use Clippy and team policy rather than ignoring warnings.

## Check your understanding

You are ready when you can point to the entry point, macro, format string, arguments, statements, and artifact profiles.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
