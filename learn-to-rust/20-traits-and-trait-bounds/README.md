# Module 20: Traits and Trait Bounds

## Outcome

Define shared capabilities with traits, implement them for types, constrain generic code, and recognize common standard traits.

## Why this matters

Generics become useful when an algorithm can say not merely any type, but any type with a capability such as formatting, comparison, cloning, iteration, or domain-specific behavior.

## Programming concept

An interface or capability contract defines operations a type promises to support. Polymorphic code can depend on that contract instead of one concrete implementation.

## Rust model

Traits define required or default methods. Types implement traits. Generic parameters can be bounded with T: Trait or where clauses. Standard traits such as Debug, Display, Clone, Default, From, Into, Iterator, Send, and Sync form much of Rust's vocabulary. Coherence rules constrain which external trait/type combinations a crate may implement.

## Local Cargo example

Create cargo new traits --edition 2024 and replace src/main.rs.

~~~rust
trait Summary {
    fn title(&self) -> &str;

    fn summarize(&self) -> String {
        format!("Summary: {}", self.title())
    }
}

struct Article {
    title: String,
}

impl Summary for Article {
    fn title(&self) -> &str {
        &self.title
    }
}

fn print_summary<T: Summary>(value: &T) {
    println!("{}", value.summarize());
}

fn main() {
    let article = Article { title: String::from("Rust traits") };
    print_summary(&article);
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- Summary is a capability contract.
- title is required while summarize has a reusable default implementation.
- Article opts into the contract with impl Summary for Article.
- print_summary is generic but only accepts types satisfying Summary.
- This is static polymorphism: the compiler retains concrete type information.

## Deliberate mistake

~~~rust
fn debug_value<T>(value: &T) {
    println!("{value:?}");
}
~~~

Debug formatting requires the Debug trait, but an unconstrained T promises no formatting capability.

Corrected direction:

~~~rust
use std::fmt::Debug;

fn debug_value<T: Debug>(value: &T) {
    println!("{value:?}");
}
~~~

## Mental model

- A trait names a capability or contract.
- Trait bounds state what generic code may assume.
- Prefer small meaningful traits over giant interfaces.
- Derive standard traits when generated behavior matches the intended semantics.
- Static trait bounds and dynamic trait objects solve different problems.

## Common mistakes

- Creating a trait for every struct without a real polymorphic need.
- Adding Clone bounds merely to bypass ownership decisions.
- Confusing Debug and Display contracts.
- Adding broad bounds to a whole type when only one method needs them.
- Assuming any foreign trait can be implemented for any foreign type.

## Transfer to other languages

Interfaces, protocols, type classes, concepts, and traits express similar capability ideas. The exact coherence and dispatch rules differ, but designing against meaningful contracts transfers broadly.

## Guided practice

1. Define a Named trait and implement it for two structs.
2. Write a generic function requiring Named.
3. Derive Debug for a small struct.
4. Rewrite several inline bounds using a where clause.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- define and implement a trait;
- use a trait bound;
- explain default methods;
- distinguish developer Debug output from user-facing Display conceptually;
- explain why traits should represent meaningful capabilities.

## Next

Continue to [Module 21](../21-lifetimes/README.md).
