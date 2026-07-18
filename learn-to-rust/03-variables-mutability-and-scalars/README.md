# Module 03: Variables, Mutability, Constants, and Scalar Types

## What you will learn

You will bind typed values, choose mutability explicitly, shadow names, and use scalar types.

```rust
fn main() {
    let title = "Rust Foundations";
    let mut module: u32 = 3;
    module += 1;
    let available = true;
    let grade = 'A';
    println!("{title} {module} {available} {grade}");
}
```

Bindings are immutable unless declared `mut`. The compiler usually infers a type, while annotations make boundaries or ambiguous conversions clear.

Integers can be signed or unsigned with fixed widths, plus `isize` and `usize` for pointer-sized indexing. Floats are `f32` or `f64`. `bool` is true or false. `char` is one Unicode scalar value and uses single quotes.

Shadowing with a new `let` can change a value and its type while preserving immutability of each binding. Mutation changes the same binding and cannot change its type.

Constants use `const`, require a type, and must be compile-time expressions. Do not hardcode deployment configuration as constants.

Integer overflow is checked in debug builds and wraps according to release behavior unless explicit checked, wrapping, saturating, or overflowing methods are used. Choose deliberately at trust boundaries.

## Check your understanding

You are ready when you can distinguish mutation, shadowing, inference, annotation, and constants.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
