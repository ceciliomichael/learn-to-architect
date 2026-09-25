# Module 30: Trait Objects and Dynamic Dispatch

## Outcome

Use dyn Trait when heterogeneous values need one runtime interface, compare static and dynamic dispatch, and recognize object-safety constraints at a practical level.

## Why this matters

Generic code chooses concrete types at compile time. Sometimes a program instead needs a collection of different concrete implementations selected at runtime, such as output sinks, plugins, formatters, or UI components.

## Programming concept

Dynamic polymorphism chooses an implementation through a runtime indirection. Static polymorphism resolves calls using concrete types during compilation. The trade includes flexibility, code organization, runtime indirection, and which type information remains available.

## Rust model

A trait object such as &dyn Draw or Box<dyn Draw> combines a pointer to a value with runtime information for calling trait methods. Box<dyn Trait> is common when heterogeneous owned implementations must share one collection. Not every trait can be made into a trait object; object-safety rules require methods to support runtime dispatch.

## Local Cargo example

Create cargo new dynamic_dispatch --edition 2024 and replace src/main.rs.

~~~rust
trait Formatter {
    fn format(&self, input: &str) -> String;
}

struct Upper;
struct Prefix {
    value: String,
}

impl Formatter for Upper {
    fn format(&self, input: &str) -> String {
        input.to_uppercase()
    }
}

impl Formatter for Prefix {
    fn format(&self, input: &str) -> String {
        format!("{}{}", self.value, input)
    }
}

fn main() {
    let formatters: Vec<Box<dyn Formatter>> = vec![
        Box::new(Upper),
        Box::new(Prefix { value: String::from("> ") }),
    ];

    for formatter in &formatters {
        println!("{}", formatter.format("rust"));
    }
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- The vector owns different concrete types behind Box.
- dyn Formatter states that callers use only the Formatter contract at this boundary.
- The concrete implementation is chosen at runtime for each element.
- This is useful because one homogeneous Vec type can hold heterogeneous implementers.
- A generic Vec<T> would instead require one concrete T for all elements.

## Deliberate mistake

~~~rust
trait Factory {
    fn create<T>(&self) -> T;
}

fn use_factory(value: &dyn Factory) {
    let _ = value;
}
~~~

A method with its own unconstrained generic result cannot be represented as a single runtime-dispatch entry in the ordinary trait-object model. Trait-object usability has method-shape restrictions.

Corrected direction:

~~~rust
trait Describe {
    fn describe(&self) -> String;
}

fn print_description(value: &dyn Describe) {
    println!("{}", value.describe());
}
~~~

## Mental model

- Use generics when callers can stay statically typed and one concrete type is known per instantiation.
- Use trait objects when heterogeneous implementations must share a runtime boundary.
- Dynamic dispatch adds pointer indirection and loses some concrete-type information at that interface.
- Do not introduce trait objects merely to look architectural.
- Keep dynamic boundaries narrow and capability-focused.

## Common mistakes

- Boxing every trait implementation by default.
- Using dyn Trait where a generic parameter is simpler.
- Creating plugin abstractions before multiple implementations or runtime selection actually exist.
- Trying to expose generic trait methods through trait objects without understanding object-safety constraints.
- Downcasting frequently, which may indicate the shared trait contract is wrong.

## Transfer to other languages

Virtual methods, interfaces, protocols, existential types, and runtime dispatch solve similar problems. Rust makes static-versus-dynamic choice explicit and keeps ownership visible.

## Guided practice

1. Create two implementations of a small trait and store them in Vec<Box<dyn Trait>>.
2. Rewrite the same operation as a generic function and compare constraints.
3. Pass &dyn Trait without allocation when ownership is unnecessary.
4. Inspect the compiler message for a deliberately non-object-safe trait.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- explain static versus dynamic dispatch;
- use Box<dyn Trait> for heterogeneous owned values;
- use &dyn Trait for borrowed dynamic behavior;
- avoid dynamic dispatch when a simpler generic or concrete design fits.

## Next

Continue to [Module 31](../31-declarative-macros/README.md).
