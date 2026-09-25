# Module 03: Values, Variables, Mutability, and Basic Types

## Outcome

Store values, choose basic scalar types, reason about immutable and mutable state, and use inference, annotations, constants, and shadowing.

## Why this matters

Programs manipulate information. Before modeling a user, file, request, or application state, you need to understand how individual values are represented and how names refer to them.

## Programming concept

A value is data. A type describes what kind of value it is and which operations make sense. A binding gives a value a name. State is information that can vary over time. Immutability prevents reassignment through a binding; mutability permits it.

## Rust model

Rust is statically typed. The compiler determines every value's type before execution. let creates an immutable binding by default, let mut permits reassignment, annotations can make a type explicit, and const defines a named compile-time constant. Shadowing uses a new let to create a new binding with the same name.

## Work in a real Cargo project

From your practice directory:

~~~text
cargo new values_and_types --edition 2024
cd values_and_types
~~~

Replace src/main.rs with:

~~~rust
const MAX_ATTEMPTS: u32 = 3;

fn main() {
    let language = "Rust";
    let mut attempts: u32 = 1;
    let temperature = 27.5;
    let ready = true;
    let symbol = 'R';

    attempts += 1;

    println!("{language} {symbol}");
    println!("attempt {attempts} of {MAX_ATTEMPTS}");
    println!("temperature: {temperature}, ready: {ready}");
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
Rust R
attempt 2 of 3
temperature: 27.5, ready: true
~~~


## Walkthrough

- language is inferred from a string literal.
- attempts is explicitly u32 and mutable.
- temperature, ready, and symbol demonstrate floating-point, Boolean, and char values.
- attempts += 1 changes one mutable binding.
- Constants require explicit types and are conventionally uppercase snake case.

## Deliberate mistake

~~~rust
fn main() {
    let attempts = 1;
    attempts = 2;
    println!("{attempts}");
}
~~~

attempts is immutable. Rust rejects reassignment through that binding. Decide whether the model truly needs changing state before adding mutability.

Corrected version:

~~~rust
fn main() {
    let mut attempts = 1;
    attempts = 2;
    println!("{attempts}");
}
~~~

Do not memorize the correction. State the rule that the original program violated.

## Mental model

- Every value has a type even when the annotation is inferred.
- Prefer immutable bindings until mutation describes the problem better.
- Inference removes redundant spelling; it does not remove types.
- Shadowing creates a new binding. Reassignment changes an existing mutable binding.
- Numeric types have finite ranges and representation rules.

## Common mistakes

- Adding mut everywhere.
- Confusing a char with a one-character string.
- Assuming integers have unlimited range.
- Thinking inference means dynamic typing.
- Using shadowing and reassignment without understanding the difference.

## Transfer to other languages

Static and dynamic languages differ in when and how types are checked, but values, representation, state, and mutation exist everywhere. Deliberately limiting mutable state is a transferable design skill.

## Guided practice

1. Create bindings for an age, temperature, Boolean flag, and character.
2. Increment one mutable counter twice.
3. Add an explicit integer annotation.
4. Shadow a trimmed string with its length and notice that the new binding can have a different type.

## Independent exercise and quiz

Complete [the exercises](exercise/exercise.md), then [the quiz](quiz/quiz.md). Attempt both before opening the answer directories.

## Readiness check

You are ready to continue when you can:

- explain value, type, binding, state, mutability, and immutability;
- use Rust scalar types;
- choose inference or an annotation deliberately;
- distinguish mutation from shadowing.

## Next

Continue to [Module 04](../04-operators-conversion-and-basic-io/README.md).
