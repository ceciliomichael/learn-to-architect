# Learn Rust: From Zero to Real Software

A local-first Rust course for people who have never programmed before and for programmers who want a deeper systems foundation.

This course uses **Rust to teach programming itself**. You will learn Rust, but the larger goal is to understand the ideas that appear across languages: values, types, control flow, functions, data modeling, errors, testing, dependencies, I/O, concurrency, networking, architecture, performance, security, and software delivery.

By the end, learning another language should feel less like starting over and more like mapping familiar concepts onto a new syntax, runtime, and ecosystem.

## Who this course is for

You do not need prior experience with:

- programming;
- terminals;
- compilers;
- Git;
- systems programming;
- C or C++;
- another programming language.

The course defines concepts before relying on them.

## How you will learn

This is not a browser-playground course. You will work on your own computer from the beginning.

You will use:

- a terminal;
- a code editor of your choice;
- `rustup`;
- stable Rust;
- Cargo;
- rustfmt;
- Clippy;
- rustdoc;
- external crates when they solve a real problem;
- Git after the basic development loop is understood.

Every runnable lesson uses a real Cargo project.

The course was rewritten in 2026 against stable Rust and the Rust 2024 edition. The development machine used while authoring the rewrite reports Rust 1.97.1 and Cargo 1.97.1. The lessons target stable Rust rather than depending on that exact patch version.

## The learning method

Each module follows the same pattern:

1. **Outcome**: what you should be able to do.
2. **Why this matters**: the problem the concept solves.
3. **Programming concept**: the idea independent of Rust.
4. **Rust model**: how Rust represents or enforces the idea.
5. **Runnable example**: code in a local Cargo project.
6. **Walkthrough**: why the code works.
7. **Deliberate mistake**: code that fails for an educational reason.
8. **Mental model**: a compact set of rules to remember.
9. **Common mistakes**: predictable beginner traps.
10. **Transfer note**: how the concept carries to other languages.
11. **Guided practice**: small focused tasks.
12. **Independent exercise**: write code without a complete solution in front of you.
13. **Quiz**: reasoning, not trivia.
14. **Readiness check**: what you should now be able to explain.
15. **Next module**: why the sequence continues where it does.

Exercises use four levels:

- **Trace** existing code.
- **Repair** broken code.
- **Modify** working code.
- **Build** a small program from requirements.

Do the work before opening the answers.

## Working rules

For each lesson:

1. Open a terminal in a practice directory.
2. Create or reuse the Cargo project named by the lesson.
3. Type the code yourself. Do not only copy and paste.
4. Predict what will happen before running it.
5. Run `cargo check`.
6. Run `cargo run` when the project is executable.
7. Use `cargo fmt`.
8. Use `cargo clippy` when the lesson introduces or requests it.
9. Read compiler diagnostics from the first relevant error.
10. Change one cause at a time when debugging.

A compiler error is information. It means the compiler has found a contradiction between the program you wrote and Rust's rules. Learning to interpret that feedback is part of learning Rust.

## Course path

### Phase 1: Learn how programs work

- [01: Set Up a Real Rust Development Environment](01-real-rust-development-environment/README.md)
- [02: Your First Program and the Compile-Run Cycle](02-first-program-and-compile-run-cycle/README.md)
- [03: Values, Variables, Mutability, and Basic Types](03-values-variables-mutability-and-types/README.md)
- [04: Operators, Conversion, and Basic Input/Output](04-operators-conversion-and-basic-io/README.md)
- [05: Expressions, Decisions, and Loops](05-expressions-decisions-and-loops/README.md)
- [06: Functions, Scope, and Decomposition](06-functions-scope-and-decomposition/README.md)
- [Checkpoint A: Command-Line Utility](projects/project-a-command-line-utility/README.md)

### Phase 2: Data and Rust's ownership model

- [07: Compound Values with Tuples and Arrays](07-tuples-arrays-and-compound-values/README.md)
- [08: Ownership, Moves, Copy, Clone, and Drop](08-ownership-moves-copy-clone-and-drop/README.md)
- [09: Borrowing and References](09-borrowing-and-references/README.md)
- [10: Strings, str, and Slices](10-strings-str-and-slices/README.md)
- [11: Structs and Methods](11-structs-and-methods/README.md)
- [12: Enums, Match, and Pattern Matching](12-enums-match-and-patterns/README.md)
- [13: Optional Values with Option](13-option-and-optional-values/README.md)
- [14: Recoverable Errors with Result](14-result-and-recoverable-errors/README.md)
- [Checkpoint B: Text and Data Processor](projects/project-b-text-data-processor/README.md)

### Phase 3: Collections, reuse, and program structure

- [15: Vectors and Dynamic Collections](15-vectors-and-dynamic-collections/README.md)
- [16: Hash Maps and Hash Sets](16-hashmaps-and-hashsets/README.md)
- [17: Modules, Crates, Packages, and Visibility](17-modules-crates-packages-and-visibility/README.md)
- [18: Testing and Testable Design](18-testing-and-testable-design/README.md)
- [19: Generics and Reusable Algorithms](19-generics-and-reusable-algorithms/README.md)
- [20: Traits and Trait Bounds](20-traits-and-trait-bounds/README.md)
- [21: Lifetimes](21-lifetimes/README.md)
- [22: Closures and Iterators](22-closures-and-iterators/README.md)
- [23: Cargo Dependencies and the Crate Ecosystem](23-cargo-dependencies-and-crates/README.md)
- [Checkpoint C: Multi-Module CLI Application](projects/project-c-multi-module-cli/README.md)

### Phase 4: Files, data formats, and application boundaries

- [24: Files, Paths, and Streamed I/O](24-files-paths-and-streamed-io/README.md)
- [25: Serialization with Serde and Untrusted Data](25-serde-and-untrusted-data/README.md)
- [26: Command-Line Interfaces, Environment, and Configuration](26-cli-environment-and-configuration/README.md)
- [27: Logging, Diagnostics, and Debugging](27-logging-diagnostics-and-debugging/README.md)
- [Checkpoint D: Persistent CLI Tool](projects/project-d-persistent-cli/README.md)

### Phase 5: Advanced ownership and abstraction

- [28: Smart Pointers with Box, Rc, and Arc](28-smart-pointers-box-rc-arc/README.md)
- [29: Drop, Deref, Cell, and RefCell](29-drop-deref-cell-refcell/README.md)
- [30: Trait Objects and Dynamic Dispatch](30-trait-objects-and-dynamic-dispatch/README.md)
- [31: Declarative Macros](31-declarative-macros/README.md)
- [32: Unsafe Rust and Safety Contracts](32-unsafe-rust-and-safety-contracts/README.md)
- [33: Foreign Function Interfaces](33-foreign-function-interfaces/README.md)

### Phase 6: Concurrency and asynchronous systems

- [34: Threads and Scoped Threads](34-threads-and-scoped-threads/README.md)
- [35: Channels and Message Passing](35-channels-and-message-passing/README.md)
- [36: Shared State with Arc, Mutex, RwLock, and Atomics](36-shared-state-and-synchronization/README.md)
- [37: Async Functions, Futures, and Tokio](37-async-futures-and-tokio/README.md)
- [38: Networking and HTTP Boundaries](38-networking-and-http-boundaries/README.md)
- [Checkpoint E: Concurrent Networked Application](projects/project-e-concurrent-networked-app/README.md)

### Phase 7: Architecture, quality, performance, and delivery

- [39: Cargo Features and Workspaces](39-cargo-features-and-workspaces/README.md)
- [40: API Design, Documentation, and Compatibility](40-api-design-documentation-and-compatibility/README.md)
- [41: Architecture and Dependency Boundaries](41-architecture-and-dependency-boundaries/README.md)
- [42: Measure and Improve Performance](42-measure-and-improve-performance/README.md)
- [43: Dependency and Supply-Chain Security](43-dependency-and-supply-chain-security/README.md)
- [44: Build, Package, Cross-Compile, and Release](44-build-package-cross-compile-and-release/README.md)
- [45: Reading Real Rust and Learning the Next Language](45-reading-real-rust-and-learning-next-language/README.md)
- [Final Capstone: Production-Style Rust Application](projects/final-capstone/README.md)

## Standard commands

You will use these often:

```text
cargo new project_name --edition 2024
cd project_name
cargo check
cargo run
cargo test
cargo fmt
cargo clippy
```

Later modules add commands such as `cargo add`, `cargo tree`, `cargo doc`, release builds, workspace commands, and security tooling.

## External crates

Real Rust development uses both the standard library and crates from the ecosystem.

This course does not hide dependencies behind copy-paste instructions. Module 23 teaches:

- what a crate is;
- how `Cargo.toml` and `Cargo.lock` work;
- `cargo add`;
- semantic versions;
- feature flags;
- direct and transitive dependencies;
- reading docs.rs and crate documentation;
- deciding whether a dependency is justified;
- basic maintenance, license, and security checks.

Only after that do later modules deliberately depend on crates such as Serde, Clap, tracing, Tokio, and an HTTP client.

## What completion means

Finishing the course does not mean memorizing every Rust API.

It means you can:

- reason about code;
- use documentation;
- understand ownership and data flow;
- model valid and invalid states;
- handle failures;
- test behavior;
- choose dependencies deliberately;
- separate business logic from external systems;
- debug with evidence;
- use concurrency without guessing;
- measure before optimizing;
- review dependencies and releases;
- read an unfamiliar Rust codebase;
- learn another language by comparing its model with what you already understand.

Start with [Module 01](01-real-rust-development-environment/README.md).
