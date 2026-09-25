# Module 22: Closures and Iterators

## Outcome

Use closures as behavior values, understand captures at a practical level, build lazy iterator pipelines, and choose loops or combinators for clarity.

## Why this matters

Many operations repeat the same traversal pattern: visit values, filter some, transform others, and combine results. Passing behavior to reusable algorithms avoids rewriting the traversal itself.

## Programming concept

A higher-order function accepts or returns behavior. An iterator represents a sequence produced over time. Lazy evaluation delays work until a consumer requests values.

## Rust model

Closures use compact syntax such as |x| x * 2 and may borrow or move captured environment values. Their call capabilities are modeled by Fn, FnMut, and FnOnce. Iterator provides next plus lazy adapters such as map and filter. Consumers such as collect, sum, count, or a for loop drive the pipeline.

## Local Cargo example

Create cargo new closures_iterators --edition 2024 and replace src/main.rs.

~~~rust
fn main() {
    let minimum = 10;
    let values = vec![4, 10, 13, 20];

    let doubled: Vec<i32> = values
        .iter()
        .copied()
        .filter(|value| *value >= minimum)
        .map(|value| value * 2)
        .collect();

    println!("{doubled:?}");
    println!("original: {values:?}");
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- The filter closure captures minimum by shared borrow.
- iter yields references and copied turns Copy elements into values.
- filter and map construct lazy adapters.
- collect drives the iterator and materializes a Vec.
- The source vector remains usable because iteration borrowed it.

## Deliberate mistake

~~~rust
fn main() {
    let values = vec![1, 2, 3];
    let mapped = values.iter().map(|x| x * 2);
    println!("mapping created");
}
~~~

Creating the map adapter does not by itself request all transformed values. The pipeline is lazy and mapped is also unused.

Corrected direction:

~~~rust
fn main() {
    let values = vec![1, 2, 3];
    let mapped: Vec<_> = values.iter().map(|x| x * 2).collect();
    println!("{mapped:?}");
}
~~~

## Mental model

- Closures package behavior and may capture surrounding state.
- Iterator adapters describe transformations lazily.
- A consumer drives item production.
- Track whether iteration yields values or references.
- Use an explicit loop when stateful control flow is clearer than a chain.

## Common mistakes

- Expecting lazy adapters to execute without a consumer.
- Building unreadable chains to appear concise.
- Using consuming iteration when the collection must remain owned.
- Cloning captured state without reasoning about borrow or move.
- Assuming every closure implements all of Fn, FnMut, and FnOnce.

## Transfer to other languages

Lambdas, closures, streams, generators, comprehensions, and iterator pipelines appear across ecosystems. Capture rules and laziness differ, but behavior-as-data is highly transferable.

## Guided practice

1. Map integers to squares and collect.
2. Filter strings by length.
3. Write a closure that mutates a captured counter.
4. Rewrite a pipeline as a for loop and compare readability.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- create and call a closure;
- explain lazy adapters versus consumers;
- track borrowed versus consuming iteration;
- choose a loop when it communicates intent better.

## Next

Continue to [Module 23](../23-cargo-dependencies-and-crates/README.md).
