# Module 41: Architecture and Dependency Boundaries

## Outcome

By the end of this module, you can separate domain policy from external I/O, design dependency direction intentionally, own application state explicitly, create useful test seams, and introduce abstractions only where change pressure justifies them.

## Why this matters

A codebase can have individually simple functions and still become difficult to change if every part directly depends on:

- files;
- HTTP;
- environment variables;
- clocks;
- databases;
- command-line parsing;
- global state;
- framework types.

When policy and mechanisms are mixed everywhere, a small requirement change spreads through the system.

Architecture is about controlling that spread.

## Programming concept

**Architecture** is the arrangement of responsibilities and dependencies.

**Separation of concerns** keeps different kinds of decisions apart.

**Dependency direction** describes which components know about which other components.

A **test seam** is a boundary where a real collaborator can be replaced with controlled behavior during tests.

**Dependency inversion** means higher-level policy can depend on an abstract capability rather than directly on one volatile mechanism.

These ideas are useful only when they make the program easier to understand and change.

They are not goals by themselves.

## Rust model

Rust gives you several architectural tools:

- modules;
- crates;
- traits;
- explicit constructors;
- ownership;
- private fields;
- Result;
- enums;
- generic parameters;
- trait objects.

The important question is not which tool looks architectural.

The question is:

**Which component should own this decision, and which direction should knowledge flow?**

## Start with policy that knows nothing about I/O

Create:

~~~text
cargo new architecture_demo --lib --edition 2024
cd architecture_demo
~~~

Put this in src/lib.rs:

~~~rust
#[derive(Debug, Clone, PartialEq, Eq)]
pub struct Greeting(String);

impl Greeting {
    pub fn text(&self) -> &str {
        &self.0
    }
}

pub trait NameSource {
    fn load_name(&self) -> Result<String, String>;
}

pub fn build_greeting(source: &dyn NameSource) -> Result<Greeting, String> {
    let name = source.load_name()?;
    let name = name.trim();

    if name.is_empty() {
        return Err(String::from("name cannot be empty"));
    }

    Ok(Greeting(format!("Hello, {name}!")))
}

#[cfg(test)]
mod tests {
    use super::*;

    struct FakeNameSource;

    impl NameSource for FakeNameSource {
        fn load_name(&self) -> Result<String, String> {
            Ok(String::from("Ada"))
        }
    }

    #[test]
    fn builds_greeting() {
        let greeting = build_greeting(&FakeNameSource).unwrap();
        assert_eq!(greeting.text(), "Hello, Ada!");
    }
}
~~~

Run:

~~~text
cargo test
~~~

## What this design is doing

Greeting is domain output.

build_greeting owns:

- trimming;
- validation;
- greeting creation.

It does not know whether the name came from:

- a file;
- an HTTP response;
- a database;
- a command-line argument;
- a test fake.

NameSource is one narrow capability boundary.

The test does not need a file or network because it substitutes a fake implementation.

## The composition root

A **composition root** is the outer place where concrete dependencies are assembled.

In a small Rust application, main is often a good composition root.

Conceptually:

~~~text
main
 |
 +--> FileNameSource
 |
 +--> build_greeting
 |
 +--> terminal output
~~~

main may know about the filesystem and terminal.

The domain function does not need to.

This keeps dependency knowledge near the outside.

## Domain versus mechanism

A useful distinction is:

~~~text
policy:
  what should the program decide?

mechanism:
  how does the program talk to an external system?
~~~

Examples:

~~~text
Policy
------
calculate discount
validate order
choose retry eligibility
classify account state

Mechanism
---------
read JSON file
send HTTP request
query database
parse CLI flags
write log event
~~~

Not every program needs a formal domain layer.

The principle is simply to avoid making core rules unnecessarily dependent on unstable external mechanisms.

## A mixed function

This function mixes several responsibilities:

~~~rust
fn calculate_price() -> Result<u64, String> {
    let raw = std::fs::read_to_string("price.txt")
        .map_err(|error| error.to_string())?;

    let value = raw
        .trim()
        .parse::<u64>()
        .map_err(|error| error.to_string())?;

    println!("price={value}");

    Ok(value)
}
~~~

It decides:

- where data comes from;
- how it is parsed;
- what the domain value is;
- how output is presented.

A smaller core is:

~~~rust
fn parse_price(raw: &str) -> Result<u64, String> {
    raw.trim()
        .parse::<u64>()
        .map_err(|error| format!("invalid price: {error}"))
}
~~~

Then an outer layer can:

1. read the file;
2. call parse_price;
3. decide what to print.

The parser can now be tested with ordinary strings.

## Dependencies should point toward stable policy

Suppose a project contains:

~~~text
cli
storage
domain
~~~

A reasonable direction may be:

~~~text
cli -------> domain
 |
 v
storage ---> domain
~~~

The domain does not know about:

- Clap;
- serde_json;
- filesystem paths;
- terminal colors.

That makes domain rules reusable and easier to test.

This is not a rule that every application must follow.

If your domain is intrinsically about a protocol or filesystem, those mechanisms may be central concepts.

Architecture follows the actual problem.

## Traits are not mandatory architecture

A common overcorrection is wrapping everything in a trait:

~~~text
UserRepository
Clock
Logger
Parser
Calculator
Formatter
Storage
Config
Environment
FileSystem
RandomProvider
~~~

Sometimes these are valuable.

Sometimes they are indirection with no real variation.

A trait is justified when it gives you something concrete such as:

- multiple implementations;
- a stable boundary around a volatile dependency;
- a useful test substitute;
- a public capability contract;
- dynamic runtime selection.

Do not create a trait merely because a function calls another function.

## Concrete dependencies are allowed

This can be perfectly good:

~~~rust
pub struct Processor {
    config: Config,
}
~~~

If Config is your own stable application type and there is no useful alternate implementation, a trait would add ceremony.

Architecture is not the elimination of concrete types.

## Test seams without over-abstraction

Sometimes pure data is the best seam.

Instead of:

~~~text
trait EnvironmentProvider
~~~

you can often do:

~~~rust
pub struct AppConfig {
    pub endpoint: String,
    pub timeout_seconds: u64,
}
~~~

Read environment variables once at the process boundary, convert them into AppConfig, then pass the owned configuration inward.

Tests construct AppConfig directly.

No fake environment interface is required.

## Own state explicitly

Avoid hidden global mutable state such as:

~~~text
global singleton cache
global mutable configuration
global current user
global database connection variable
~~~

Hidden global state makes it harder to know:

- who can mutate it;
- when it changes;
- which tests depend on it;
- how concurrency is synchronized;
- how multiple application instances could coexist.

Prefer state owned by:

- main;
- an application struct;
- a worker task;
- a service object;
- another clearly responsible component.

Then pass access explicitly.

## One owner can simplify concurrency

A useful architecture is sometimes:

~~~text
many callers
    |
    v
bounded channel
    |
    v
one state-owning worker
    |
    v
state
~~~

Instead of:

~~~text
many callers
    |
    v
Arc<Mutex<large shared state>>
~~~

Both are valid tools.

The better model depends on:

- interaction shape;
- latency requirements;
- contention;
- failure behavior;
- shutdown;
- ownership clarity.

Architecture and concurrency design are connected.

## Errors cross boundaries too

A filesystem adapter may produce:

~~~text
std::io::Error
~~~

The domain may care only about:

~~~text
NotFound
Unavailable
InvalidStoredData
~~~

An adapter can translate external errors into application-level categories.

Do not erase useful diagnostic cause unnecessarily.

Do not leak every infrastructure-specific type throughout domain APIs if callers do not need it.

## Deliberate mistake

Suppose domain code directly imports:

~~~rust
use clap::Parser;
use reqwest::Client;
use serde_json::Value;
~~~

even though its responsibility is calculating invoice totals.

Now tests and reuse are coupled to mechanisms unrelated to invoice arithmetic.

A better dependency boundary is:

~~~text
CLI / HTTP / JSON
       |
       v
adapter or orchestration
       |
       v
validated domain inputs
       |
       v
invoice rules
~~~

## Mental model

- Put decisions near the responsibility that owns them.
- Keep stable policy independent from volatile mechanisms when practical.
- Compose concrete dependencies near the outside.
- Prefer explicit ownership of application state.
- Create abstractions at real seams, not everywhere.
- Pure data can be a better boundary than a trait.
- Translate external representations before they spread inward.
- Keep error meaning appropriate to the layer.
- Architecture should reduce change cost, not maximize layers.

## Common mistakes

### Interface for everything

This produces ceremony and hides simple call relationships.

### One giant application service

A single type can become another global object containing every responsibility.

### Domain objects that are actually database rows

Persistence representation and domain meaning are not always the same contract.

### Framework types everywhere

When every layer accepts framework-specific request, JSON, database, or CLI types, changing the mechanism becomes expensive.

### Global state to avoid parameter passing

Passing dependencies explicitly may feel repetitive, but it makes ownership and coupling visible.

### Copying a named architecture mechanically

Ports and adapters, clean architecture, hexagonal architecture, layered architecture, and functional core/imperative shell are useful patterns.

None of them replaces understanding your system.

## Transfer to other languages

These concepts transfer directly across languages and frameworks.

You may see names such as:

- dependency injection;
- ports and adapters;
- hexagonal architecture;
- clean architecture;
- layered architecture;
- onion architecture;
- functional core, imperative shell.

The useful common idea is controlling dependencies and side effects.

## Guided practice

1. Take one function that mixes file I/O and calculation.
2. Extract a pure parsing or calculation function.
3. Move environment reading to the process boundary.
4. Pass a configuration struct inward.
5. Create one trait only where a genuine external capability needs substitution.
6. Draw dependency arrows for Checkpoint D.
7. Identify one dependency arrow you would remove if requirements changed.

## Exercise and quiz

Complete the exercises and quiz before checking answers.

- [Exercises](exercise/exercise.md)
- [Quiz](quiz/quiz.md)

## Readiness check

You are ready to continue when you can:

- distinguish policy from mechanism;
- draw dependency direction;
- keep domain logic free from unnecessary I/O dependencies;
- compose infrastructure at the outside;
- identify a real test seam;
- choose between a trait and plain data;
- avoid hidden global mutable state;
- explain why more layers do not automatically mean better architecture.

## Next

Continue to [Module 42](../42-measure-and-improve-performance/README.md).
