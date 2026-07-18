# Module 06: Ownership, Moves, Copy, and Clone

## What you will learn

You will trace who owns a value, recognize moves, and distinguish cheap copying from explicit deep duplication.

```rust
fn main() {
    let first = String::from("Rust");
    let second = first;
    println!("{second}");
}
```

`String` owns heap data. Assignment moves that ownership to `second`, so using `first` afterward is rejected. This prevents both bindings from freeing the same allocation.

Types such as integers and booleans implement `Copy`, so assignment copies their complete value and both bindings remain usable. `Copy` is implicit and limited to types safe for bitwise duplication.

`clone` explicitly duplicates data when the type supports it. Cloning can allocate and hide cost, so use it only when two independent owners are required.

Passing to a function follows the same rules. Returning can transfer ownership back. At the end of an owner's scope, Rust runs `drop` automatically.

Ownership is a compile-time model. The compiler may optimize storage, but reason from language ownership rather than guessed stack and heap locations.

## Check your understanding

You are ready when you can mark each move, copy, clone, and drop point in a short program.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
