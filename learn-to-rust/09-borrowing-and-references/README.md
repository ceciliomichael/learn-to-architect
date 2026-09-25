# Module 09: Borrowing and References

## Outcome

Borrow values without taking ownership, use shared and mutable references, and reason about Rust's aliasing rules.

## Why this matters

Moving ownership into every function would be inconvenient. Often a function only needs temporary access. References allow temporary access while preserving a clear owner.

## Programming concept

A reference is a way to access a value owned elsewhere. Aliasing means multiple access paths refer to the same underlying value. Mutation becomes dangerous when multiple aliases can read or write unpredictably, so languages need rules around shared access.

## Rust model

&T is a shared reference and allows read-only access. &mut T is a mutable reference and permits mutation. At a given point, Rust allows many shared references or one active mutable reference to the same data, not conflicting access. The compiler also prevents references from outliving the values they borrow.

## Local Cargo example

~~~text
cargo new borrowing --edition 2024
cd borrowing
~~~

Replace src/main.rs:

~~~rust
fn length(text: &String) -> usize {
    text.len()
}

fn add_mark(text: &mut String) {
    text.push('!');
}

fn main() {
    let mut message = String::from("hello");

    let size = length(&message);
    println!("length before: {size}");

    add_mark(&mut message);
    println!("message: {message}");
}
~~~

Run cargo check, cargo run, and cargo fmt.

Expected output:

~~~text
length before: 5
message: hello!
~~~


## Walkthrough

- message remains owned by main.
- &message creates temporary shared access for length.
- The shared borrow ends after its last use, so a later mutable borrow is allowed.
- &mut message gives add_mark exclusive mutable access for the relevant borrow.
- The owner can use message again after the mutable borrow ends.

## Deliberate mistake

~~~rust
fn main() {
    let mut text = String::from("hello");
    let first = &mut text;
    let second = &mut text;

    first.push('!');
    second.push('?');
}
~~~

Two mutable references would permit overlapping writers to the same value. Rust rejects the second conflicting borrow while the first remains in use.

Corrected version:

~~~rust
fn main() {
    let mut text = String::from("hello");

    {
        let first = &mut text;
        first.push('!');
    }

    let second = &mut text;
    second.push('?');

    println!("{text}");
}
~~~

## Mental model

- Ownership answers who is responsible for the value. Borrowing answers who may access it temporarily.
- Shared borrows permit observation without mutation through that reference.
- A mutable borrow requires exclusive access for its active use.
- Borrows can end before the surrounding lexical scope when they are no longer used.
- References must never outlive their referents.

## Common mistakes

- Cloning instead of borrowing when temporary access is enough.
- Holding a mutable borrow longer than necessary.
- Trying to mutate through a shared reference.
- Assuming braces are always required to end a borrow; modern Rust tracks last use precisely.
- Thinking a reference owns the referent.

## Transfer to other languages

Aliasing and mutation matter in every language. Other languages may enforce rules by convention, runtime checks, locks, immutability, or garbage collection. Rust makes many of these access relationships compile-time obligations.

## Guided practice

1. Write a function that reads a String through a shared reference.
2. Write a function that appends through a mutable reference.
3. Create two shared references and use both.
4. Attempt conflicting mutable/shared use and read the diagnostic carefully.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before reading the answers.

## Readiness check

- distinguish owner and borrower;
- use &T and &mut T;
- state the many-readers-or-one-writer rule at a useful beginner level;
- explain why dangling references are rejected.

## Next

Continue to [Module 10](../10-strings-str-and-slices/README.md).
