# Module 08: Ownership, Moves, Copy, Clone, and Drop

## Outcome

Trace which binding owns a resource, recognize moves and Copy behavior, use Clone deliberately, and explain deterministic cleanup.

## Why this matters

Programs create resources that must eventually be released: allocated memory, files, sockets, locks, and more. Languages need a strategy for deciding how long those resources remain valid and who is responsible for cleanup.

## Programming concept

Ownership is responsibility for a resource's lifetime. Copying can mean duplicating a small value or creating a second independent resource. Moving transfers responsibility. Cleanup should occur exactly when the owner no longer needs the resource.

## Rust model

Most Rust values have one owner. Assigning an owned non-Copy value such as String normally moves ownership. Simple types that implement Copy are duplicated implicitly. Clone is an explicit request to make an independent duplicate when supported. When an owner leaves scope, Rust runs its Drop behavior automatically. Reason from ownership rules, not guesses about whether a variable physically lives on a stack or heap.

## Local Cargo example

~~~text
cargo new ownership_basics --edition 2024
cd ownership_basics
~~~

Replace src/main.rs:

~~~rust
fn main() {
    let original = String::from("Rust");
    let moved = original;

    let number = 7;
    let copied_number = number;

    let first = String::from("independent");
    let cloned = first.clone();

    println!("moved: {moved}");
    println!("numbers: {number}, {copied_number}");
    println!("strings: {first}, {cloned}");
}
~~~

Run cargo check, cargo run, and cargo fmt.

Expected output:

~~~text
moved: Rust
numbers: 7, 7
strings: independent, independent
~~~


## Walkthrough

- String owns growable text storage, so assigning original to moved transfers ownership.
- Using original after that move is rejected.
- Integers such as i32 implement Copy, so both number bindings remain usable.
- clone explicitly duplicates the String's owned data.
- At the end of scope, each currently owned String is cleaned up once.

## Deliberate mistake

~~~rust
fn main() {
    let first = String::from("hello");
    let second = first;

    println!("{first}");
    println!("{second}");
}
~~~

Ownership of the String moved into second. Allowing first to keep acting as an owner would permit two owners to believe they should clean up the same resource.

Corrected version:

~~~rust
fn main() {
    let first = String::from("hello");
    let second = first;

    println!("{second}");
}
~~~

## Mental model

- Ask who owns each non-Copy value at this point in the program.
- A move transfers ownership; it does not perform an expensive deep copy.
- Copy types deliberately behave like inexpensive value duplication.
- Clone is explicit because it may allocate or perform meaningful work.
- Cleanup follows ownership and scope.

## Common mistakes

- Adding clone whenever the compiler reports a move.
- Thinking every assignment copies data deeply.
- Explaining ownership only as stack versus heap placement.
- Assuming Copy is available for any type you want.
- Trying to manually free ordinary Rust values.

## Transfer to other languages

Garbage-collected languages automate memory reclamation differently, but ownership of files, locks, transactions, handles, and mutable state still matters. Move semantics and deterministic cleanup also appear in other systems languages.

## Guided practice

1. Move a String and confirm the old binding is rejected.
2. Copy an integer and use both bindings.
3. Clone a String and mutate one copy later after strings are reviewed.
4. Pass a String into a function by value and observe that ownership moves into the call.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before reading the answers.

## Readiness check

- identify the owner of a String at each step;
- distinguish move, Copy, and Clone;
- explain why use-after-move is rejected;
- connect scope end with deterministic cleanup.

## Next

Continue to [Module 09](../09-borrowing-and-references/README.md).
