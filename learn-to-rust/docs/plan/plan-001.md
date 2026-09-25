# Plan 001: End-to-End 2026 Learn Rust Rewrite

## Status

Implemented. The end-to-end rewrite is materialized in the repository. The root README is the canonical course index.

## Goal

Rebuild this repository into a complete local-first Rust course for a learner with no prior programming knowledge.

The course must do two things at the same time:

1. Teach Rust from first principles through advanced, production-oriented topics.
2. Teach transferable programming and software-engineering mental models so that learning Rust makes later languages easier to understand.

Rust is the teaching language, but programming itself is the larger subject.

## Core learner promise

A learner who completes the course should be able to:

- use a real terminal, editor, Rust toolchain, and Cargo project without relying on a browser playground;
- explain how source code becomes a running program;
- understand values, types, state, control flow, functions, data structures, modules, errors, tests, I/O, concurrency, networking, and program architecture;
- understand Rust-specific ownership, borrowing, lifetimes, traits, smart pointers, unsafe Rust, and FFI;
- read compiler errors and debug problems methodically instead of guessing;
- design and build small programs independently;
- progress from a single-file command-line program to a multi-crate, tested, observable, releasable application;
- recognize which concepts are universal and which are Rust-specific;
- approach another language by mapping its syntax and runtime model onto concepts already learned here.

## Teaching principles

### 1. Local development is the default

The course will not use the Rust Playground as the learning workflow.

From Module 01 onward, the learner works on their own computer with:

- a terminal;
- a code editor;
- rustup;
- stable Rust;
- Cargo;
- rustfmt;
- Clippy;
- rustdoc;
- Git when version-control concepts are introduced.

Every runnable lesson will use an actual local Cargo project.

### 2. Assume zero programming knowledge

Terms such as compiler, variable, expression, stack, heap, process, thread, API, dependency, serialization, and runtime must be explained before being relied on.

Do not write explanations that only make sense to someone who already knows Python, JavaScript, C, Java, or another language.

### 3. Teach the concept before the shortcut

Examples:

- understand matching a Result before leaning on ?;
- understand loops before iterator chains;
- understand ownership before recommending clone;
- understand threads before async;
- understand concrete types and generics before trait objects;
- understand safe abstractions before unsafe Rust.

Convenience syntax should feel like compression of an understood idea, not magic.

### 4. Compiler errors are part of the curriculum

Learners should intentionally encounter and repair errors.

For important concepts, lessons should show:

1. code that looks reasonable;
2. the relevant compiler complaint in summarized form;
3. what rule was violated;
4. how to reason to the repair;
5. the corrected code.

Do not train learners to copy the compiler suggestion blindly.

### 5. Separate universal programming ideas from Rust-specific rules

Every module should identify:

- **Programming concept:** the idea that transfers to other languages;
- **Rust model:** how Rust represents or enforces it;
- **Transfer note:** what may differ in another language.

Example:

- Programming concept: values have lifetimes and resources need owners.
- Rust model: ownership and borrowing are checked statically.
- Transfer note: garbage-collected languages manage reclamation differently, but aliasing, mutation, resource lifetime, and concurrency still matter.

### 6. Use progressive disclosure

Begin with the smallest correct mental model. Add exceptions and advanced details only when the learner has enough context to use them.

Avoid front-loading every edge case.

### 7. Make examples realistic without making them large

Use small programs with believable data and behavior:

- unit converters;
- command-line prompts;
- text analysis;
- inventories;
- task lists;
- configuration files;
- log processing;
- HTTP clients;
- worker queues.

Avoid meaningless examples unless they demonstrate one very small syntax point.

### 8. Repetition should be cumulative

Important concepts must reappear later in new contexts.

Ownership should reappear in collections, closures, threads, async, smart pointers, and API design rather than existing only in Modules 08 to 10.

## 2026 baseline

The rewrite should target:

- Rust stable;
- Rust 2024 edition;
- local Cargo workflows;
- the installed environment currently reports Rust 1.97.1 and Cargo 1.97.1.

Lessons should avoid depending unnecessarily on one exact compiler patch version. When a minimum Rust version matters, state it explicitly.

Third-party crates should be introduced only when the standard library no longer provides the practical capability being taught.

## Course structure

The existing repository has good topical breadth but is too compressed for a zero-experience learner. The rewrite should preserve useful coverage while reorganizing the learning sequence and expanding explanation and practice.

Final implementation structure: 45 core modules plus cumulative checkpoint projects.

During implementation, a dedicated Module 23, Cargo Dependencies and the Crate Ecosystem, was added before dependency-heavy application topics. The original numbered outline below was the planning sequence, so modules that originally followed Module 22 are shifted by one in the final repository. Use the root README for canonical final numbering.

### Phase 1: Learn how programs work

#### Module 01: Set Up a Real Rust Development Environment
- What programming is.
- What source code is.
- Terminal and filesystem basics needed by the course.
- Install rustup and stable Rust.
- Verify rustc, cargo, rustfmt, and Clippy.
- Create a working directory.
- Create, build, run, check, and format a Cargo project.
- Learn the basic Cargo project layout.

Transferable concepts:
- toolchains;
- command-line workflows;
- source trees;
- build tools.

#### Module 02: Your First Program and the Compile-Run Cycle
- Read main.rs.
- fn main.
- statements and expressions at a very basic level.
- println!.
- strings and punctuation.
- source -> compiler -> executable -> process.
- compile-time error versus runtime behavior.
- intentionally break and repair code.

Transferable concepts:
- entry points;
- syntax;
- compilation;
- processes;
- feedback loops.

#### Module 03: Values, Variables, Mutability, and Basic Types
- let.
- immutability by default.
- mut.
- integer, floating-point, boolean, and char values.
- type inference.
- explicit type annotations.
- constants.
- shadowing.
- overflow expectations in debug and release at a beginner-safe level.

Transferable concepts:
- values;
- state;
- types;
- mutable versus immutable state.

#### Module 04: Operators, Conversion, and Basic Input/Output
- arithmetic and comparison.
- boolean logic.
- precedence.
- explicit numeric conversion.
- stdin and stdout.
- reading text.
- parsing text into a number.
- simple input validation.

Transferable concepts:
- data transformation;
- parsing;
- representation;
- external input boundaries.

#### Module 05: Expressions, Decisions, and Loops
- expression-oriented Rust.
- if and else.
- loop.
- while.
- for.
- ranges.
- break with a value.
- continue.
- introduction to match without advanced patterns.

Transferable concepts:
- branching;
- repetition;
- control flow;
- state machines at a basic level.

#### Module 06: Functions, Scope, and Decomposition
- declaring and calling functions.
- parameters.
- return values.
- expressions versus statements.
- scopes.
- local variables.
- simple call-stack mental model.
- small pure functions.
- decomposition and naming.

Transferable concepts:
- abstraction;
- interfaces between pieces of code;
- local reasoning;
- decomposition.

### Checkpoint Project A: Command-Line Utility

Build a small interactive utility such as a unit converter or score calculator.

Requirements:
- real Cargo project;
- user input;
- parsing;
- functions;
- conditions;
- loops;
- clear errors for invalid input;
- cargo fmt;
- cargo clippy;
- manual test cases.

The learner should build most of it without copying a complete final program.

---

### Phase 2: Data and Rust's ownership model

#### Module 07: Compound Values with Tuples and Arrays
- tuples.
- destructuring.
- fixed-size arrays.
- indexing.
- bounds.
- when fixed-size data is useful.

Transferable concepts:
- aggregate data;
- indexing;
- fixed versus dynamic collections.

#### Module 08: Ownership, Moves, Copy, Clone, and Drop
- why resource lifetime is a programming problem.
- String as owned data.
- moves.
- Copy.
- Clone.
- scope and drop.
- passing and returning ownership.
- why Rust rejects use-after-move.

Transferable concepts:
- resource ownership;
- value semantics;
- copying cost;
- deterministic cleanup.

#### Module 09: Borrowing and References
- shared references.
- mutable references.
- borrowing rules.
- reborrowing at a beginner-appropriate level.
- preventing dangling references.
- why exclusive mutation matters.

Transferable concepts:
- aliasing;
- mutation;
- references;
- data access contracts.

#### Module 10: Strings, str, and Slices
- String versus &str.
- string literals.
- byte representation and UTF-8.
- slices.
- array and vector slices.
- why string indexing is restricted.
- common string operations.

Transferable concepts:
- owned versus borrowed views;
- text encoding;
- contiguous data;
- boundaries and indexing.

#### Module 11: Structs and Methods
- define structs.
- instantiate values.
- field access.
- update syntax.
- tuple structs.
- impl.
- methods.
- associated functions.
- borrowing self.

Transferable concepts:
- records;
- data modeling;
- behavior attached to data;
- invariants.

#### Module 12: Enums, Match, and Pattern Matching
- enum variants.
- variants with data.
- exhaustive match.
- if let and let else.
- destructuring patterns.
- catch-all patterns.
- modeling state with enums.

Transferable concepts:
- sum types;
- finite states;
- exhaustive decision making.

#### Module 13: Optional Values with Option
- why absence must be modeled.
- Some and None.
- matching first.
- common combinators after the basic model is clear.
- when unwrap and expect are appropriate or inappropriate.

Transferable concepts:
- nullability;
- explicit absence;
- invalid-state prevention.

#### Module 14: Recoverable Errors with Result
- Ok and Err.
- matching Result.
- error propagation.
- ?.
- error context.
- panic versus recoverable failure.
- basic custom error enums.
- boundaries between internal errors and user-facing messages.

Transferable concepts:
- failure as data;
- error propagation;
- error boundaries;
- recoverability.

### Checkpoint Project B: Text and Data Processor

Build a local text-processing application.

Possible behavior:
- read commands or a file;
- normalize and analyze text;
- return useful errors;
- model results with structs and enums;
- use borrowing rather than unnecessary cloning;
- test invalid input.

The project should force repeated ownership and borrowing decisions.

---

### Phase 3: Collections, reuse, and program structure

#### Module 15: Vectors and Dynamic Collections
- Vec<T>.
- push and remove.
- indexing versus get.
- iteration.
- mutable iteration.
- ownership when iterating.
- capacity at an introductory level.

Transferable concepts:
- dynamic arrays;
- collection growth;
- iteration;
- safe access.

#### Module 16: Hash Maps and Hash Sets
- key-value data.
- uniqueness.
- insert, get, entry.
- ownership of keys and values.
- hashing conceptually.
- when map/set/vector are appropriate.

Transferable concepts:
- associative containers;
- uniqueness;
- lookup tradeoffs.

#### Module 17: Modules, Crates, Packages, and Visibility
- files and modules.
- mod.
- use.
- pub.
- crate roots.
- binary versus library crates.
- Cargo packages.
- public versus private APIs.

Transferable concepts:
- namespaces;
- encapsulation;
- module boundaries;
- package organization.

#### Module 18: Testing and Testable Design
- unit tests.
- integration tests.
- assertions.
- expected failures.
- testing Result.
- test organization.
- deterministic tests.
- what tests can and cannot prove.
- testable function design.

Transferable concepts:
- verification;
- regression protection;
- seams and boundaries;
- deterministic behavior.

#### Module 19: Generics and Reusable Algorithms
- generic functions.
- generic structs and enums.
- monomorphization conceptually.
- when generic code improves reuse.
- when concrete code is clearer.

Transferable concepts:
- parametric polymorphism;
- reusable algorithms;
- compile-time abstraction.

#### Module 20: Traits and Trait Bounds
- defining traits.
- implementing traits.
- default methods.
- trait bounds.
- where clauses.
- standard traits such as Debug, Display, Clone, Default, From, and Into at appropriate depth.
- orphan-rule intuition.

Transferable concepts:
- interfaces;
- contracts;
- capability-based design.

#### Module 21: Lifetimes
- what problem lifetimes describe.
- lifetime elision.
- function lifetime relationships.
- structs borrowing data.
- 'static.
- common lifetime error reasoning.
- prefer ownership when borrowing relationships add needless complexity.

Transferable concepts:
- object lifetime;
- reference validity;
- API lifetime contracts.

#### Module 22: Closures and Iterators
- closures.
- capture.
- Fn, FnMut, FnOnce at conceptual depth.
- Iterator.
- map, filter, find, fold, collect.
- lazy evaluation.
- loops versus iterator pipelines.
- ownership effects.

Transferable concepts:
- higher-order functions;
- lazy pipelines;
- functional transformation.

### Checkpoint Project C: Multi-Module CLI Application

Build a task, inventory, or notes application.

Requirements:
- library plus binary structure;
- multiple modules;
- structs and enums;
- Vec and HashMap where justified;
- Result-based error handling;
- unit and integration tests;
- reusable generic or trait-based code only where it genuinely helps;
- no unnecessary clone calls.

---

### Phase 4: Files, data formats, and application boundaries

#### Module 23: Files, Paths, and Streamed I/O
- Path and PathBuf.
- open/create/read/write.
- BufReader and BufWriter.
- line-oriented processing.
- filesystem errors.
- safe temporary-file thinking.
- path portability.

Transferable concepts:
- storage boundaries;
- streams;
- buffering;
- operating-system resources.

#### Module 24: Serialization with Serde and Untrusted Data
- why serialization exists.
- JSON as the first format.
- Serialize and Deserialize.
- schema expectations.
- validate after deserialization.
- size and nesting limits conceptually.
- never trust external data.

Transferable concepts:
- wire/storage formats;
- parsing boundaries;
- validation;
- schema evolution.

#### Module 25: Command-Line Interfaces, Environment, and Configuration
- command-line arguments.
- environment variables.
- configuration precedence.
- secrets versus ordinary config.
- exit codes.
- stdout versus stderr.
- introduce a CLI crate only after manual argument concepts are understood.

Transferable concepts:
- process interfaces;
- configuration boundaries;
- automation-friendly programs.

#### Module 26: Logging, Diagnostics, and Debugging
- println debugging versus structured diagnostics.
- dbg!.
- log levels.
- tracing concepts.
- backtraces.
- reading compiler diagnostics.
- narrowing a bug.
- reproducible bug reports.
- debugger introduction where practical.

Transferable concepts:
- observability;
- diagnosis;
- reproducibility.

### Checkpoint Project D: Persistent CLI Tool

Extend the prior application or build a new one that:

- accepts real command-line arguments;
- persists data in JSON;
- validates loaded data;
- uses files safely;
- has clear exit behavior;
- records useful diagnostics;
- has automated tests.

---

### Phase 5: Advanced ownership and abstraction

#### Module 27: Smart Pointers with Box, Rc, and Arc
- why pointer-like ownership types exist.
- Box for heap ownership and recursive types.
- Rc for shared single-thread ownership.
- Arc for shared thread-safe ownership.
- reference counts and cycles.

Transferable concepts:
- indirection;
- shared ownership;
- heap allocation;
- reference counting.

#### Module 28: Drop, Deref, Cell, and RefCell
- RAII.
- Drop.
- Deref.
- interior mutability.
- Cell.
- RefCell runtime borrow checking.
- panic risks from invalid dynamic borrows.
- when interior mutability is justified.

Transferable concepts:
- resource guards;
- proxy types;
- runtime enforcement;
- controlled mutation.

#### Module 29: Trait Objects and Dynamic Dispatch
- dyn Trait.
- object safety basics.
- Box<dyn Trait>.
- static versus dynamic dispatch.
- extensibility tradeoffs.

Transferable concepts:
- dynamic polymorphism;
- runtime dispatch;
- plugin-style boundaries.

#### Module 30: Declarative Macros
- why macros exist.
- macro_rules!.
- token patterns.
- repetition.
- hygiene conceptually.
- when a function or generic is better.
- procedural macros as awareness, not an immediate deep implementation requirement.

Transferable concepts:
- code generation;
- metaprogramming;
- syntax extension.

#### Module 31: Unsafe Rust and Safety Contracts
- what unsafe permits.
- raw pointers.
- unsafe functions.
- unsafe traits.
- mutable statics and unions conceptually.
- undefined behavior.
- safety invariants.
- safe wrappers.
- SAFETY comments.
- Miri where supported.

Transferable concepts:
- trusted computing boundaries;
- invariants;
- memory models;
- proof obligations.

#### Module 32: Foreign Function Interfaces
- ABI concept.
- extern.
- C-compatible types.
- ownership across boundaries.
- strings and buffers.
- error transfer.
- panic containment.
- safe wrapper design.

Transferable concepts:
- language interoperability;
- ABI boundaries;
- cross-language ownership contracts.

---

### Phase 6: Concurrency and asynchronous systems

#### Module 33: Threads and Scoped Threads
- processes versus threads.
- spawn and join.
- move closures.
- scoped threads.
- data races.
- Send and Sync conceptually.
- CPU-bound parallelism versus concurrency.

Transferable concepts:
- concurrency;
- parallelism;
- isolation;
- scheduling.

#### Module 34: Channels and Message Passing
- producer and consumer.
- channels.
- ownership transfer through messages.
- shutdown signaling.
- bounded versus unbounded queues conceptually.
- backpressure.

Transferable concepts:
- message passing;
- queues;
- work distribution;
- flow control.

#### Module 35: Shared State with Arc, Mutex, RwLock, and Atomics
- Mutex.
- lock guards.
- poisoning conceptually.
- avoiding deadlocks.
- RwLock.
- atomics at a careful introductory level.
- choose message passing versus shared state.

Transferable concepts:
- synchronization;
- mutual exclusion;
- memory coordination;
- contention.

#### Module 36: Async Functions, Futures, and Tokio
- Future mental model.
- async fn.
- await.
- executor/runtime.
- Tokio.
- spawning tasks.
- cancellation.
- timeouts.
- blocking work.
- async does not make CPU work automatically faster.

Transferable concepts:
- cooperative concurrency;
- event loops;
- asynchronous I/O;
- cancellation.

#### Module 37: Networking and HTTP Boundaries
- sockets conceptually.
- clients and servers.
- HTTP request/response mental model.
- timeouts.
- retries and idempotency.
- status codes.
- body size limits.
- TLS as a required production concern.
- use a maintained HTTP crate rather than implementing production HTTP by hand.

Transferable concepts:
- network boundaries;
- protocols;
- partial failure;
- distributed-system assumptions.

### Checkpoint Project E: Concurrent Networked Application

Build either:

- a concurrent HTTP client/worker; or
- a small service with a deliberately narrow API.

Requirements:
- cancellation or clean shutdown;
- bounded concurrency;
- timeout handling;
- structured errors;
- logging/tracing;
- tests around business logic;
- external I/O kept behind clear boundaries.

---

### Phase 7: Architecture, quality, performance, and delivery

#### Module 38: Cargo Features and Workspaces
- feature flags.
- optional dependencies.
- additive feature design.
- workspaces.
- multiple crates.
- dependency placement.
- avoiding unnecessary feature combinations.

Transferable concepts:
- modular builds;
- package graphs;
- optional capabilities.

#### Module 39: API Design, Documentation, and Compatibility
- public API surface.
- rustdoc.
- examples as documentation.
- semantic versioning.
- compatibility thinking.
- newtype patterns.
- making invalid states difficult to represent.
- error type design.
- extension without needless abstraction.

Transferable concepts:
- interface design;
- contracts;
- compatibility;
- maintainability.

#### Module 40: Architecture and Dependency Boundaries
- separate domain logic from I/O.
- dependency direction.
- ports/adapters as a concept, without forcing a framework.
- state ownership.
- configuration boundary.
- test seams.
- avoid global mutable state.
- choose abstractions only when change pressure justifies them.

Transferable concepts:
- architecture;
- separation of concerns;
- dependency management;
- change isolation.

#### Module 41: Measure and Improve Performance
- debug versus release.
- measure before optimizing.
- benchmarking.
- allocation awareness.
- algorithmic complexity.
- profiling.
- copies and clones.
- cache and locality concepts.
- optimization tradeoffs.

Transferable concepts:
- profiling;
- complexity;
- bottleneck analysis;
- evidence-based optimization.

#### Module 42: Dependency and Supply-Chain Security
- Cargo.lock.
- direct and transitive dependencies.
- reviewing crates.
- cargo tree.
- vulnerability and advisory tooling.
- license awareness.
- minimal dependency policy.
- reproducible dependency resolution.
- secrets and build pipelines.

Transferable concepts:
- software supply chains;
- dependency trust;
- provenance;
- risk reduction.

#### Module 43: Build, Package, Cross-Compile, and Release
- release builds.
- locked builds.
- target triples.
- cross-compilation limitations.
- artifact inspection.
- checksums.
- version and commit metadata.
- CI concepts.
- rollback planning.
- library packaging versus application delivery.

Transferable concepts:
- build pipelines;
- artifacts;
- deployment;
- reproducibility;
- rollback.

#### Module 44: Reading Real Rust and Learning the Next Language
- read unfamiliar crate code systematically.
- inspect Cargo.toml first.
- find entry points.
- trace types and ownership.
- use rustdoc and source navigation.
- compare Rust concepts with garbage-collected, interpreted, object-oriented, and dynamically typed languages.
- identify syntax differences versus semantic differences.
- build a language-learning checklist for the learner's next language.

Transferable concepts:
- language acquisition;
- codebase navigation;
- semantic mapping;
- independent learning.

### Final Capstone: Production-Style Rust Application

The final capstone should not be a toy one-file project.

Recommended shape:

- Cargo workspace or well-structured package;
- command-line interface;
- domain layer separated from external I/O;
- persistent local data or an HTTP boundary;
- serialization;
- configuration;
- structured errors;
- unit and integration tests;
- logging/tracing;
- concurrency where justified;
- documentation;
- Clippy-clean code;
- release build;
- dependency review;
- a short architecture document explaining major decisions and tradeoffs.

The capstone should include milestones rather than a full copy-paste solution.

## Standard module format

Every module should follow a predictable structure.

### 1. Title and outcome

State exactly what the learner will be able to do by the end.

### 2. Why this matters

Explain the problem before introducing Rust syntax.

### 3. Programming concept

Explain the language-independent idea.

### 4. Rust model

Explain how Rust expresses or checks the idea.

### 5. First runnable example

Use a complete local Cargo example.

Always show:
- file path;
- code;
- command to run;
- expected output when deterministic.

### 6. Walkthrough

Explain important lines and connect them to the mental model.

### 7. Deliberate mistake

Provide at least one meaningful broken example for concepts where compiler feedback is educational.

### 8. Build the mental model

State the rules in plain language.

For complex topics, include diagrams using text when useful.

### 9. Common mistakes

Explain likely beginner errors and why they happen.

### 10. Transfer note

State what carries into other languages and what is Rust-specific.

### 11. Guided practice

Small tasks that isolate the new concept.

### 12. Independent exercise

A task that requires the learner to write code without being given the final implementation.

### 13. Quiz

Test reasoning, not trivia.

Include code-reading and prediction questions where useful.

### 14. Summary and readiness check

Give a short checklist of what the learner should now be able to explain or build.

### 15. Next module

Explain why the next topic follows naturally.

## Exercise design standard

Exercises should progress through four levels:

1. **Trace:** predict what existing code does.
2. **Repair:** fix intentionally broken code.
3. **Modify:** change a working program to meet a new requirement.
4. **Build:** create a small solution from a written requirement.

Not every module needs a large exercise, but every major concept should include at least one task where the learner writes code without a provided skeleton.

Solutions must explain reasoning, not just show final code.

## Quiz design standard

Quizzes should test understanding rather than memorized syntax.

Use a mixture of:

- explain in plain language;
- predict compile or reject;
- predict output;
- identify ownership or borrowing relationships;
- select a data model and justify it;
- compare two approaches;
- identify a failure boundary;
- explain why a tempting solution is unsafe, fragile, or unnecessarily complex.

Answers must explain why the correct answer is correct and why common alternatives fail.

## Project progression

The course should repeatedly build complete software, not only isolated snippets.

- Project A: interactive command-line utility.
- Project B: ownership-heavy text/data processor.
- Project C: tested multi-module application.
- Project D: persistent configurable CLI.
- Project E: concurrent networked application.
- Final Capstone: production-style application.

Each project should reuse prior concepts and introduce very little brand-new syntax by itself.

## Repository changes expected during implementation

The implementation phase should:

- rewrite the root README as the course landing page;
- remove Playground-first instructions;
- rename the first module away from "playground";
- renumber/reorganize modules to match the approved curriculum;
- rewrite every lesson README;
- rewrite every exercise;
- rewrite every exercise solution;
- rewrite every quiz;
- rewrite every quiz answer;
- add checkpoint-project directories;
- add any small starter code needed by exercises;
- keep learner code local and Cargo-based;
- ensure all code samples target Rust 2024 edition;
- compile and test runnable examples where practical.

Do not preserve old wording simply to reduce diff size. Preserve only material that still serves the new teaching model.

## Writing style

- beginner-readable English;
- define terms before using them;
- short sections;
- concrete examples before abstractions;
- no unexplained jargon;
- no fake simplicity that hides important rules;
- no excessive analogies;
- no claims that Rust makes all programs safe or bug-free;
- clearly distinguish compile-time guarantees from runtime and business-logic correctness;
- avoid encouraging clone, unwrap, unsafe, Arc<Mutex<_>>, macros, or async as default solutions.

## Rewrite execution order

Implementation should happen in controlled phases.

### Pass 1: Foundation
- rewrite root README;
- establish module template;
- rewrite Modules 01 to 06;
- implement Project A;
- verify commands and code.

### Pass 2: Ownership and modeling
- rewrite Modules 07 to 14;
- implement Project B;
- compile ownership/borrowing examples and deliberate failures.

### Pass 3: Reusable programs
- rewrite Modules 15 to 22;
- implement Project C;
- verify tests and module layouts.

### Pass 4: Real application boundaries
- rewrite Modules 23 to 26;
- implement Project D;
- verify file, serialization, CLI, and diagnostic examples.

### Pass 5: Advanced Rust
- rewrite Modules 27 to 32;
- verify smart-pointer, macro, unsafe, and FFI examples carefully.

### Pass 6: Concurrency and networking
- rewrite Modules 33 to 37;
- implement Project E;
- test shutdown, timeouts, and concurrency examples.

### Pass 7: Architecture and delivery
- rewrite Modules 38 to 44;
- create final capstone;
- complete release and next-language material.

### Pass 8: Whole-course quality audit
- validate all links;
- search for stale module numbers and old Playground references;
- run rustfmt on code projects;
- run cargo check/test/clippy where applicable;
- verify solution links;
- verify quizzes match lessons;
- verify every new term is introduced before being assumed;
- verify transfer notes exist and are useful;
- read the full course sequentially for pacing and duplication.

## Acceptance criteria

The rewrite is complete only when:

- a person with no prior programming experience can start at Module 01 without an unexplained prerequisite;
- the normal path never requires an online Playground;
- every module uses a consistent learning structure;
- every runnable workflow works from a local Cargo project;
- ownership and borrowing are explained progressively and reused throughout the course;
- advanced topics build on concepts already taught;
- each phase contains meaningful hands-on work;
- all major concepts include transferable programming lessons;
- exercises require active coding and reasoning;
- solutions explain reasoning;
- quizzes test understanding;
- examples compile on the chosen stable Rust baseline unless deliberately marked as compile-fail examples;
- no lesson treats compiler acceptance as proof that business logic, security, or external data is correct;
- the final capstone requires design, testing, observability, and release practices;
- the final module explicitly teaches the learner how to transfer what they learned to another programming language.

## Explicit non-goals

The course should not:

- become a catalog of every Rust API;
- teach frameworks before fundamentals;
- depend on an IDE-specific workflow;
- rely on browser sandboxes;
- make async the default programming model;
- encourage abstraction for its own sake;
- turn advanced Rust into mandatory complexity when a safe simple design is sufficient;
- claim mastery after syntax alone.

## Proposed next action

After this plan is reviewed, begin Pass 1 only:

1. rewrite the root README;
2. rename/rebuild Module 01 around local workstation setup;
3. rewrite Modules 02 to 06;
4. add Checkpoint Project A;
5. validate every example locally before continuing to ownership.
