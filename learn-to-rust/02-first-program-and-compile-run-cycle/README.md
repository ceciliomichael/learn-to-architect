# Module 02: Your First Program and the Compile-Run Cycle

## Outcome

Read a tiny Rust program, explain how source becomes a running process, and distinguish compile-time rejection from runtime behavior.

## Why this matters

Before adding language features, you need a precise picture of what happens when you run a program. That picture becomes the foundation for debugging, dependencies, testing, optimization, and deployment.

## Programming concept

A program begins as source code. A language implementation translates or executes that source. A runnable compiled artifact is an executable. A running instance is a process. Compile-time checks happen before that process starts; runtime behavior happens after it starts.

## Rust model

Rust is normally compiled ahead of time. Cargo invokes the compiler, which parses source, resolves names, checks types and Rust's other static rules, then produces machine code when the program is valid. Successful compilation proves those checks passed, not that your intended behavior is correct.

## Work in a real Cargo project

From your practice directory:

~~~text
cargo new compile_cycle --edition 2024
cd compile_cycle
~~~

Replace src/main.rs with:

~~~rust
fn main() {
    println!("source -> compiler -> executable -> process");
    println!("Compilation can reject code before it runs.");
}
~~~

Run:

~~~text
cargo check
cargo run
cargo fmt
~~~

Expected output:

~~~text
source -> compiler -> executable -> process
Compilation can reject code before it runs.
~~~


## Walkthrough

- main is the entry point of this binary.
- Braces group the function body.
- Each println invocation is used as a statement and ends with a semicolon.
- A quoted value is a string literal.
- The exclamation mark is macro-call syntax. Macros are taught later; println is simply the standard printing tool for now.

## Deliberate mistake

~~~rust
fn main() {
    println!("Hello")
    println!("Rust")
}
~~~

The compiler cannot correctly separate the two statements because the first invocation is missing its semicolon. No new process starts from this invalid source.

Corrected version:

~~~rust
fn main() {
    println!("Hello");
    println!("Rust");
}
~~~

Do not memorize the correction. State the rule that the original program violated.

## Mental model

- Write source, check it, build it, then run the result.
- Compile time and runtime are different phases.
- Compiler acceptance is not proof that the program meets its requirements.
- Small edit-check-run cycles make mistakes easier to isolate.

## Common mistakes

- Calling every failure a runtime error.
- Assuming compiled means correct.
- Changing many lines after one diagnostic.
- Memorizing punctuation without understanding statement boundaries.

## Transfer to other languages

Interpreted and just-in-time compiled languages use different pipelines, but source representation, translation or execution, and runtime behavior still exist. The exact compile-time boundary varies by language.

## Guided practice

1. Change one printed string and run again.
2. Introduce an unmatched quote and read the first diagnostic.
3. Run cargo build and inspect target/debug.
4. Explain what cargo run adds after ensuring the build is current.

## Independent exercise and quiz

Complete [the exercises](exercise/exercise.md), then [the quiz](quiz/quiz.md). Attempt both before opening the answer directories.

## Readiness check

You are ready to continue when you can:

- identify a Rust binary entry point;
- describe source to compiler to executable to process;
- distinguish compile-time rejection from runtime behavior;
- explain why compilation cannot prove business correctness.

## Next

Continue to [Module 03](../03-values-variables-mutability-and-types/README.md).
