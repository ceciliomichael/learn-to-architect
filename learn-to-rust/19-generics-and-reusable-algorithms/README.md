# Module 19: Generics and Reusable Algorithms

## Outcome

Parameterize functions and data structures over types without erasing type safety, and recognize when concrete code is clearer than abstraction.

## Why this matters

Many algorithms and containers do not care about one exact concrete type. Rewriting the same structure for integers, strings, and domain objects creates duplication.

## Programming concept

Parametric polymorphism expresses logic using a type parameter. Callers instantiate that parameter with concrete types. Abstraction is valuable when behavior is genuinely shared, not merely because two pieces of code look similar.

## Rust model

Generic parameters use angle brackets such as T. A generic type can store T without knowing one concrete type in its definition. Operations on T require explicit capabilities, which Rust expresses with traits in the next module. Rust usually monomorphizes generic code into concrete compiled forms where used.

## Local Cargo example

Create cargo new generics --edition 2024 and replace src/main.rs.

~~~rust
struct Pair<T> {
    first: T,
    second: T,
}

impl<T> Pair<T> {
    fn first(&self) -> &T {
        &self.first
    }

    fn second(&self) -> &T {
        &self.second
    }
}

fn first_item<T>(values: &[T]) -> Option<&T> {
    values.first()
}

fn main() {
    let numbers = Pair { first: 10, second: 20 };
    let words = ["rust", "generic"];

    println!("{}", numbers.first());
    println!("{}", numbers.second());
    println!("{:?}", first_item(&words));
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- Pair<T> says both fields use one caller-selected type T.
- The impl is generic over that same T.
- Borrowed getters avoid moving an unknown non-Copy value out of a shared reference.
- first_item works for slices of any element type because first needs no type-specific operation.
- The compiler still knows the concrete type at each use.

## Deliberate mistake

~~~rust
fn add<T>(a: T, b: T) -> T {
    a + b
}
~~~

The compiler cannot assume every possible T supports addition. Generic code can use only operations guaranteed for all types allowed by its constraints.

Corrected direction:

~~~rust
fn first_item<T>(values: &[T]) -> Option<&T> {
    values.first()
}
~~~

## Mental model

- A generic parameter stands for a concrete type selected by use.
- Generic does not mean dynamically typed.
- Only perform operations justified for every allowed T.
- Abstract repeated concepts, not accidental textual similarity.
- Trait bounds add required capabilities and come next.

## Common mistakes

- Making code generic before a reuse pattern exists.
- Assuming T supports printing, cloning, comparison, or arithmetic.
- Using generics when domain concepts should stay intentionally separate.
- Trying to move an unknown T out of a shared reference.
- Thinking generic code loses static type information.

## Transfer to other languages

Generics, templates, and type parameters appear across statically typed languages. Runtime implementation varies, but the design question is the same: which parts vary by type and which capabilities are required?

## Guided practice

1. Create Wrapper<T>.
2. Write last_item<T> returning Option<&T>.
3. Instantiate Pair with String.
4. Try to debug-print an unconstrained T and read the diagnostic.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- define a generic struct and function;
- explain that generic uses still have concrete types;
- identify an operation that needs a capability constraint;
- avoid unnecessary generic abstraction.

## Next

Continue to [Module 20](../20-traits-and-trait-bounds/README.md).
