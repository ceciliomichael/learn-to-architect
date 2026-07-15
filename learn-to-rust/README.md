# Learn Rust Step by Step

This course teaches programming with Rust from the beginning. You do not need prior programming or command-line experience.

Rust is a statically typed, compiled language. Its compiler checks types, ownership, and borrowing before a program runs. Rust can prevent many memory and concurrency mistakes, but it cannot prove that business rules, permissions, or external data are correct. This course teaches both its guarantees and its boundaries.

Complete the modules in order. Ownership ideas are introduced slowly and reused consistently.

## Two ways to run the examples

### Option 1: Use the official Rust Playground

Open the [Rust Playground](https://play.rust-lang.org/), keep **Stable** selected, replace the example, and select **Run**. Use **Tools**, then **Rustfmt**, to format code. Use **Clippy** when the lesson asks for extra feedback.

The Playground is the simplest option for early modules. It runs in a browser and can compile either a small program or a test. It has no network access and limits execution time, memory, and disk use. It offers only selected third-party crates. Lessons clearly say when a local Cargo project is required.

### Option 2: Work on your computer

Install Rust through <https://rustup.rs/>. This installs the compiler, Cargo, formatting tools, and documentation management.

Check the stable toolchain:

```text
rustc --version
cargo --version
rustup show
```

Create and run a Rust 2024 edition project:

```text
cargo new rust-practice --edition 2024
cd rust-practice
cargo run
```

Format and check it with:

```text
cargo fmt --check
cargo clippy --all-targets --all-features
```

Core examples target stable Rust 1.90 and newer. Local Cargo is required for multi-file crates, dependencies, tests, files, networks, async work, workspaces, and release artifacts.

## How every module is organized

Each module contains:

1. A lesson in `README.md`
2. Guided work in `exercise/exercise.md`
3. A short quiz in `quiz/quiz.md`
4. Complete exercise solutions in `answers/exercise/exercise-solutions.md`
5. Explained quiz answers in `answers/quiz/quiz-answers.md`

Type examples yourself. Predict whether they compile and what they print. When the compiler rejects code, read the primary message and the suggested source location before editing.

## Course path

### First programs and decisions

- [Module 01: Use the Rust Playground and Install Rust](01-playground-install-and-cargo/README.md)
- [Module 02: Compile and Run Your First Program](02-first-program-and-compilation/README.md)
- [Module 03: Variables, Mutability, Constants, and Scalar Types](03-variables-mutability-and-scalars/README.md)
- [Module 04: Expressions, Conditions, Loops, and Match Basics](04-expressions-and-control-flow/README.md)
- [Module 05: Functions, Scope, and Tuples](05-functions-scope-and-tuples/README.md)

### Ownership and data modeling

- [Module 06: Ownership, Moves, Copy, and Clone](06-ownership-moves-copy-clone/README.md)
- [Module 07: Borrow with References](07-borrowing-and-references/README.md)
- [Module 08: Slices, str, and String](08-slices-str-and-string/README.md)
- [Module 09: Structs and Methods](09-structs-and-methods/README.md)
- [Module 10: Enums, Match, and Patterns](10-enums-match-and-patterns/README.md)
- [Module 11: Optional Values with Option](11-option/README.md)
- [Module 12: Recoverable Errors with Result](12-result-and-errors/README.md)

### Collections, modules, and reusable code

- [Module 13: Vectors and Iteration](13-vectors-and-iteration/README.md)
- [Module 14: Hash Maps and Hash Sets](14-hashmaps-and-hashsets/README.md)
- [Module 15: Modules, Crates, Packages, and Visibility](15-modules-crates-and-visibility/README.md)
- [Module 16: Test Rust Code](16-testing/README.md)
- [Module 17: Generics and Const Generics](17-generics-and-const-generics/README.md)
- [Module 18: Traits and Trait Bounds](18-traits-and-trait-bounds/README.md)
- [Module 19: Lifetimes](19-lifetimes/README.md)
- [Module 20: Closures and Iterators](20-closures-and-iterators/README.md)

### Managed memory and I/O

- [Module 21: Smart Pointers with Box, Rc, and Arc](21-smart-pointers-box-rc-and-arc/README.md)
- [Module 22: Drop, Deref, Cell, and RefCell](22-drop-deref-cell-and-refcell/README.md)
- [Module 23: Trait Objects and Dynamic Dispatch](23-trait-objects-and-dynamic-dispatch/README.md)
- [Module 24: Files, Paths, and Streamed I/O](24-files-paths-and-streamed-io/README.md)
- [Module 25: Serde and Untrusted Data](25-serde-and-untrusted-data/README.md)

### Concurrent and asynchronous work

- [Module 26: Threads and Scoped Threads](26-threads-and-scoped-threads/README.md)
- [Module 27: Channels, Arc, Mutex, and Shared State](27-channels-arc-mutex-and-shared-state/README.md)
- [Module 28: Async Functions, Futures, and Tokio](28-async-futures-and-tokio/README.md)
- [Module 29: Networking and HTTP Boundaries](29-networking-and-http-boundaries/README.md)

### Maintainable tools and advanced language features

- [Module 30: Command-Line Programs, Configuration, and Logging](30-command-line-configuration-and-logging/README.md)
- [Module 31: Declarative Macros](31-declarative-macros/README.md)
- [Module 32: Unsafe Rust and Safety Contracts](32-unsafe-rust-and-safety-contracts/README.md)
- [Module 33: Foreign Function Interfaces](33-foreign-function-interfaces/README.md)
- [Module 34: Cargo Features and Workspaces](34-cargo-features-and-workspaces/README.md)
- [Module 35: Documentation, API Design, and Compatibility](35-documentation-api-design-and-compatibility/README.md)
- [Module 36: Measure and Improve Performance](36-measure-and-improve-performance/README.md)
- [Module 37: Dependency and Supply-Chain Security](37-dependency-and-supply-chain-security/README.md)
- [Module 38: Build, Package, and Release Rust Programs](38-build-package-and-release/README.md)

## Safety and study habits

Use disposable projects and non-sensitive data. Do not paste unfamiliar dependencies into `Cargo.toml` without checking their source and maintenance. Keep `unsafe` code isolated and documented. Use release builds only after debug behavior and tests are correct.
