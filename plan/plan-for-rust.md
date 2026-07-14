# Plan for the Rust Learning Module

## Purpose

This document tracks `learn-to-rust/`, a beginner-to-advanced Rust course for learners with no programming experience.

The course begins in the official Rust Playground. It moves to Cargo when learners need multi-file crates, dependencies, tests, files, networking, async work, workspaces, documentation, and release builds. Core examples use stable Rust 1.90 and newer with the Rust 2024 edition. They will be verified with the installed Rust 1.94.0 toolchain.

The course will not contain a miscellaneous module or final assessment.

## Teaching decisions

1. Explain compilation and `main` before ownership terminology.
2. Teach ordinary values and control flow before borrowing.
3. Separate moves, shared borrowing, mutable borrowing, and slices.
4. Teach structs before methods and enums before `Option` and `Result` workflows.
5. Teach concrete collections before generics and traits.
6. Teach ownership-based resource cleanup before smart pointers.
7. Teach threads before shared synchronization and async work.
8. Keep `unsafe` late and require a written safety contract.
9. Validate all external data before it enters domain behavior.
10. Treat dependency selection and release artifacts as security boundaries.

## Required module structure

```text
module-NN-topic/
|-- README.md
|-- exercise/
|   `-- exercise.md
|-- quiz/
|   `-- quiz.md
`-- answers/
    |-- exercise/
    |   `-- exercise-solutions.md
    `-- quiz/
        `-- quiz-answers.md
```

Every lesson uses plain language, no emoji, and no em dash characters. Exercises are complete, repeatable, and explained.

## Course roadmap

### Part 1: First programs and decisions

- [x] **Module 01: Use the Rust Playground and Install Rust**
  - Official Playground, sandbox limits, stable channel, rustup, `rustc`, Cargo, version checks, files, formatting, and compiler messages.
- [x] **Module 02: Compile and Run Your First Program**
  - `fn main`, statements, expressions preview, macros, `println!`, comments, `rustc`, Cargo packages, debug and release builds.
- [x] **Module 03: Variables, Mutability, Constants, and Scalar Types**
  - Immutable bindings, `mut`, shadowing, constants, integers, floats, booleans, characters, type inference, and annotations.
- [x] **Module 04: Expressions, Conditions, Loops, and Match Basics**
  - Expression values, `if`, `else`, `loop`, `while`, `for`, ranges, `break` values, labels, and simple `match`.
- [x] **Module 05: Functions, Scope, and Tuples**
  - Parameters, return expressions, blocks, tuple values, destructuring, unit, early return, and focused functions.

### Part 2: Ownership and data modeling

- [x] **Module 06: Ownership, Moves, Copy, and Clone**
  - Stack and heap intuition, ownership rules, moves, `Copy`, explicit `clone`, drops, and function transfer.
- [x] **Module 07: Borrow with References**
  - Shared and mutable references, borrowing rules, scopes, reborrowing, dangling-reference prevention, and mutation contracts.
- [x] **Module 08: Slices, str, and String**
  - String ownership, UTF-8, string slices, array and vector slices, valid boundaries, indexing rejection, and safe iteration.
- [x] **Module 09: Structs and Methods**
  - Named, tuple, and unit structs, field shorthand, update syntax and moves, methods, associated functions, invariants, and borrowing receivers.
- [x] **Module 10: Enums, Match, and Patterns**
  - Data-carrying variants, exhaustive matching, destructuring, guards, `if let`, `let else`, and domain states.
- [x] **Module 11: Optional Values with Option**
  - `Some`, `None`, matching, combinators, borrowing options, defaults, and avoiding sentinel values.
- [x] **Module 12: Recoverable Errors with Result**
  - `Ok`, `Err`, `?`, error propagation, custom error enums, source chains, panic boundaries, and user-facing reporting.

### Part 3: Collections, modules, and reusable code

- [x] **Module 13: Vectors and Iteration**
  - Creation, growth, indexing choices, borrowing, mutation, slices, iterators preview, and invalidation prevention.
- [x] **Module 14: Hash Maps and Hash Sets**
  - Ownership of entries, lookup, entry API, updates, iteration, hashing, set operations, and nondeterministic order.
- [x] **Module 15: Modules, Crates, Packages, and Visibility**
  - Library and binary crates, modules, paths, `use`, `pub`, re-exports, package layout, and dependency direction.
- [x] **Module 16: Test Rust Code**
  - Unit and integration tests, assertions, expected errors, test results, temporary boundaries, documentation tests, and isolation.
- [x] **Module 17: Generics and Const Generics**
  - Generic functions and types, monomorphization, bounds preview, const parameters, and when concrete code is clearer.
- [x] **Module 18: Traits and Trait Bounds**
  - Shared behavior, implementations, default methods, bounds, `impl Trait`, associated types, orphan rules, and API design.
- [x] **Module 19: Lifetimes**
  - Reference relationships, elision, function and struct annotations, static lifetime meaning, and avoiding unnecessary annotations.
- [x] **Module 20: Closures and Iterators**
  - Closure capture modes, `Fn` traits, iterator adaptors, ownership choices, laziness, collection, and readable chains.

### Part 4: Managed memory and I/O

- [x] **Module 21: Smart Pointers with Box, Rc, and Arc**
  - Heap ownership, recursive data, shared ownership, reference counts, thread safety, cycles, and choosing the smallest tool.
- [x] **Module 22: Drop, Deref, Cell, and RefCell**
  - RAII cleanup, deref coercion, interior mutability, runtime borrow checks, cycles, and single-threaded boundaries.
- [x] **Module 23: Trait Objects and Dynamic Dispatch**
  - `dyn Trait`, object safety, heterogeneous collections, static versus dynamic dispatch, downcasting restraint, and plugin boundaries.
- [x] **Module 24: Files, Paths, and Streamed I/O**
  - `Path`, `PathBuf`, files, buffered I/O, UTF-8, bytes, permissions, cleanup, bounded reads, and atomic replacement.
- [x] **Module 25: Serde and Untrusted Data**
  - Dependency setup, serialization, deserialization, field rules, unknown fields, validation types, size limits, and schema boundaries.

### Part 5: Concurrent and asynchronous work

- [x] **Module 26: Threads and Scoped Threads**
  - Spawning, moving data, joining, scoped borrowing, panic results, task ownership, and avoiding detached work.
- [x] **Module 27: Channels, Arc, Mutex, and Shared State**
  - Message passing, multiple producers, channel closure, mutex poisoning, lock scope, atomics preview, and deadlock avoidance.
- [x] **Module 28: Async Functions, Futures, and Tokio**
  - Future laziness, `.await`, runtime responsibilities, tasks, structured joins, cancellation safety, timeouts, and blocking work.
- [x] **Module 29: Networking and HTTP Boundaries**
  - TCP basics, maintained HTTP clients, URL parsing, timeouts, bounded bodies, status handling, TLS defaults, and validated responses.

### Part 6: Maintainable tools and advanced language features

- [x] **Module 30: Command-Line Programs, Configuration, and Logging**
  - Arguments, environment input, typed configuration, exit status, stdout and stderr, structured logs, secret redaction, and tests.
- [x] **Module 31: Declarative Macros**
  - Pattern matching, repetition, hygiene, fragments, useful small macros, diagnostics, and preferring functions when possible.
- [x] **Module 32: Unsafe Rust and Safety Contracts**
  - Raw pointers, unsafe operations, safe wrappers, invariants, aliasing, initialization, layout, and tools for checking assumptions.
- [x] **Module 33: Foreign Function Interfaces**
  - C ABI, representation, ownership across boundaries, strings, errors, callbacks, build scripts, platform concerns, and isolation.
- [x] **Module 34: Cargo Features and Workspaces**
  - Optional behavior, additive features, resolver behavior, workspace dependencies, lock files, profiles, and avoiding feature misuse.
- [x] **Module 35: Documentation, API Design, and Compatibility**
  - Rustdoc, examples, documentation tests, public contracts, sealed choices, semantic versioning, deprecation, and migration.
- [x] **Module 36: Measure and Improve Performance**
  - Release builds, representative timing, profiling, allocation awareness, iterator costs, code size, and evidence-based optimization.
- [x] **Module 37: Dependency and Supply-Chain Security**
  - Minimal dependencies, lock files, advisories, licenses, build scripts, proc macros, review, updates, and reproducible CI.
- [x] **Module 38: Build, Package, and Release Rust Programs**
  - Artifacts, target triples, cross-compilation boundaries, metadata, publishing checks, stripped binaries, provenance, and rollback.

## Dependency rules

1. No borrowing appears before ownership transfer is explained.
2. No string slicing appears without UTF-8 boundary rules.
3. No `Option` or `Result` shortcut appears before matching the enum directly.
4. No iterator chain appears before loops and collection ownership.
5. No lifetime annotation appears before ordinary borrowing.
6. No smart pointer appears before direct ownership and references.
7. No shared concurrency appears before thread joining and ownership transfer.
8. No async task is started without a completion, cancellation, or shutdown policy.
9. No external data is trusted merely because deserialization succeeded.
10. No unsafe block appears without a stated invariant and safe boundary.
11. No dependency is added without explaining trust and maintenance cost.
12. No performance claim is made from debug builds or one unrepresentative run.

## Verification checklist

- [x] Confirm official Rust Playground, Book, Cargo, and edition guidance
- [x] Create the Rust root README with online and local options
- [x] Create Modules 01 through 08
- [x] Create Modules 09 through 16
- [x] Create Modules 17 through 25
- [x] Create Modules 26 through 32
- [x] Create Modules 33 through 38
- [x] Verify all required folders and files
- [x] Check every relative Markdown link
- [x] Check code fences, ASCII-only writing, and unfinished markers
- [x] Format complete Rust examples with `rustfmt`
- [x] Compile complete standalone examples with Rust 1.94.0
- [x] Run representative Cargo tests, Clippy checks, concurrency, async, and release builds
- [x] Update the repository root README
- [x] Mark every roadmap item complete

## Definition of done

The course is complete when all 38 modules exist in the required structure, early examples work in the official Playground where stated, Cargo examples use Rust 2024 edition correctly, ownership prerequisites remain ordered, exercises have complete answers, unsafe and external boundaries are explicit, and all repository audits pass.
