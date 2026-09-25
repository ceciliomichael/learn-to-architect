# Module 17: Modules, Crates, Packages, and Visibility

## Outcome

Split code across modules and files, distinguish modules, crates, and packages, and design public versus private boundaries.

## Why this matters

As a program grows, organization becomes design. Good boundaries let you understand and change one responsibility without loading the entire codebase into your head.

## Programming concept

Namespaces organize names. Encapsulation hides implementation details behind a smaller interface. Packages are distribution/build units, while module hierarchies organize source inside compilation units.

## Rust model

A Cargo package is described by Cargo.toml and can contain crate targets. A crate is one Rust compilation unit with a root such as src/main.rs or src/lib.rs. Modules form a namespace tree inside a crate. mod declares modules, use shortens paths, and pub widens visibility from the default private boundary.

## Local Cargo example

Create cargo new organizer --edition 2024. Add src/lib.rs and src/report.rs, keeping src/main.rs.

~~~rust
// src/lib.rs
pub mod report;

// src/report.rs
pub struct Summary {
    title: String,
}

impl Summary {
    pub fn new(title: impl Into<String>) -> Self {
        Self { title: title.into() }
    }

    pub fn title(&self) -> &str {
        &self.title
    }
}

// src/main.rs
use organizer::report::Summary;

fn main() {
    let summary = Summary::new("Weekly");
    println!("{}", summary.title());
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- The package contains a library crate and a binary crate.
- lib.rs is the library root and declares report.
- Summary is public while title remains private.
- new and title form a small public API.
- main imports the library item through its crate path.

## Deliberate mistake

~~~rust
mod account {
    pub struct Account {
        balance: i64,
    }
}

fn main() {
    let a = account::Account { balance: 10 };
    println!("{}", a.balance);
}
~~~

A public struct does not automatically expose its fields. The module still owns the private balance field.

Corrected direction:

~~~rust
mod account {
    pub struct Account {
        balance: i64,
    }

    impl Account {
        pub fn new(balance: i64) -> Self { Self { balance } }
        pub fn balance(&self) -> i64 { self.balance }
    }
}

fn main() {
    let a = account::Account::new(10);
    println!("{}", a.balance());
}
~~~

## Mental model

- Package, crate, and module are distinct layers.
- Default privacy is useful: expose only what callers need.
- Organize by responsibility, not arbitrary file size.
- Library logic is easier to test and reuse than logic trapped in main.
- Public API is a compatibility commitment.

## Common mistakes

- Calling every source file a crate.
- Making everything pub to fix errors.
- Mirroring folders without meaningful boundaries.
- Putting all logic in main.
- Exposing fields when methods could enforce invariants.

## Transfer to other languages

Packages, modules, namespaces, assemblies, and visibility rules differ, but encapsulation and dependency boundaries are universal.

## Guided practice

1. Move a struct into a module file.
2. Create lib.rs and call library code from main.rs.
3. Keep a field private and expose a getter.
4. Draw the module tree.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- distinguish package, crate, and module;
- split a crate across files;
- use pub deliberately;
- explain why small public surfaces protect change.

## Next

Continue to [Module 18](../18-testing-and-testable-design/README.md).
