# Module 19: Lifetimes

References must never outlive the values they borrow. Rust usually proves this without extra writing. A lifetime annotation is needed when a function or type must explain how multiple references are related.

```rust
fn longer<'a>(left: &'a str, right: &'a str) -> &'a str {
    if left.len() >= right.len() {
        left
    } else {
        right
    }
}
```

`'a` does not extend either string's life. It tells the compiler that the returned reference is valid only for the part of the program where both inputs are valid.

A struct that stores a reference also states that relationship:

```rust
struct Label<'a> {
    text: &'a str,
}
```

Lifetime elision rules cover common functions such as `fn first_word(text: &str) -> &str`. Write annotations only when the relationship is ambiguous or part of a type definition.

`'static` means a reference can remain valid for the entire program. String literals have this property because they are stored in the compiled program. It does not mean every value should be leaked or kept forever.

Avoid returning a reference to a local value. Return the owned value instead. Ownership is often simpler than adding difficult lifetime relationships.

## A useful reading method

When a lifetime error appears, ask three questions: who owns the value, who borrows it, and how long does the returned reference need to remain usable? Shortening a borrow or returning ownership often reveals the cleanest solution.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 20](../20-closures-and-iterators/README.md).
