# Module 04: Expressions, Conditions, Loops, and Match Basics

## What you will learn

You will use expression values and choose or repeat program paths.

```rust
fn main() {
    let score = 82;
    let label = if score >= 90 {
        "excellent"
    } else if score >= 75 {
        "good"
    } else {
        "practice"
    };
    println!("{label}");
}
```

An `if` condition must be `bool`. Each branch used as a value must produce the same type. The final expression has no semicolon because its value leaves the block.

Rust has `loop`, `while`, and `for`. `break value` can make a `loop` produce a result. Ranges such as `1..5` exclude 5, while `1..=5` includes it. Labels can target an outer loop but should remain rare.

`match` compares a value against exhaustive patterns:

```rust
fn main() {
    let message = match 2 {
        1 => "one",
        2 => "two",
        _ => "other",
    };
    println!("{message}");
}
```

The wildcard handles all remaining values. Rich enum patterns arrive later. Do not use `_` to hide a domain case that deserves explicit treatment.

## Check your understanding

You are ready when you can predict expression values, range endpoints, loop termination, and exhaustive matching.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
