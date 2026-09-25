# Module 15: Vectors and Dynamic Collections

## Outcome

Use Vec for growable sequences, access elements safely, iterate by shared or mutable borrow, and understand when iteration moves ownership.

## Why this matters

Arrays have a fixed length. Many programs discover the number of items only at runtime: task lists, parsed records, search results, and queued jobs need dynamic collections.

## Programming concept

A dynamic array stores an ordered sequence that can grow or shrink. It tracks a logical length and usually some allocated capacity. Collection APIs must define whether access borrows elements, mutates them, or removes ownership.

## Rust model

Vec<T> is Rust's growable contiguous collection. push appends, pop removes from the end, get returns Option for checked access, and indexing can panic when a position is invalid. Iteration can borrow, mutably borrow, or consume the vector.

## Local Cargo example

Create cargo new vectors --edition 2024, enter it, and replace src/main.rs.

~~~rust
fn main() {
    let mut scores = vec![70, 82, 91];
    scores.push(88);

    if let Some(first) = scores.first() {
        println!("first: {first}");
    }

    for score in &mut scores {
        *score += 1;
    }

    for score in &scores {
        println!("{score}");
    }

    println!("count: {}", scores.len());
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- vec! creates a vector with initial values.
- push mutates the collection and may grow its allocation.
- first returns Option<&T>, so empty vectors do not require a panic.
- Mutable iteration yields mutable references to elements.
- Shared iteration borrows the vector, so it remains usable afterward.

## Deliberate mistake

~~~rust
fn main() {
    let values = vec![1, 2, 3];
    for value in values {
        println!("{value}");
    }
    println!("{}", values.len());
}
~~~

The loop iterates by value and consumes the vector, so values is no longer available afterward.

Corrected direction:

~~~rust
fn main() {
    let values = vec![1, 2, 3];
    for value in &values {
        println!("{value}");
    }
    println!("{}", values.len());
}
~~~

## Mental model

- Use Vec when ordered sequence length changes at runtime.
- Choose get when an index is uncertain.
- Ask whether iteration borrows, mutably borrows, or consumes.
- Growth can reallocate backing storage, so references into a vector cannot be assumed stable across mutation.
- Capacity is a storage resource, not the logical element count.

## Common mistakes

- Indexing with user-controlled positions without checking.
- Cloning only because a loop consumed the vector.
- Keeping an element reference while trying to push.
- Confusing len with capacity.
- Using Vec when key lookup or uniqueness is the real model.

## Transfer to other languages

Dynamic arrays appear under many names. Growth, capacity, indexing behavior, and ownership vary, but ordered runtime-sized storage is a common abstraction.

## Guided practice

1. Push and pop values.
2. Use get with valid and invalid positions.
3. Try shared, mutable, and consuming iteration separately.
4. Compare len and capacity after reserving space.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- choose Vec for a growable ordered sequence;
- use checked access for uncertain positions;
- predict iteration ownership;
- distinguish length from capacity.

## Next

Continue to [Module 16](../16-hashmaps-and-hashsets/README.md).
