# Module 01: Set Up a Real Rust Development Environment

## Outcome

Install or verify the Rust toolchain, navigate a terminal, create a Cargo project, and understand the files Cargo creates.

## Why this matters

Programming is not only writing text in an editor. A real development workflow includes source files, a compiler, a build tool, generated artifacts, and commands that you can repeat. Learning that workflow now prevents the tooling from feeling mysterious later.

## Programming concept

A **toolchain** is the set of programs used to turn source code into runnable software. A **terminal** is a text interface for starting programs and working with files. A **project directory** is simply a folder that contains the files for one piece of software.

## Rust model

Rust is normally installed with **rustup**, which manages Rust toolchains. **rustc** is the compiler. **Cargo** creates projects, resolves dependencies, builds code, runs tests, and manages common development tasks. **rustfmt** formats Rust code and **Clippy** provides additional lint checks.

## Work in a real Cargo project

From your practice directory:

```text
cargo new rust_setup_check --edition 2024
cd rust_setup_check
```

Replace `src/main.rs` with:

```rust
fn main() {
    println!("My local Rust toolchain works.");
}
```

Then run:

```text
cargo check
cargo run
cargo fmt
```

Expected output:

```text
My local Rust toolchain works.
```

## Walkthrough

- `fn main()` is the entry point of this executable program. You do not need to understand functions yet.
- `println!` asks the program to write a line to standard output.
- `cargo check` checks the project quickly without producing the final executable you normally run.
- `cargo run` builds the executable when needed and then starts it.
- `target/` contains generated build output. Your source belongs in `src/`, not in `target/`.

## Deliberate mistake

Try this version or change in your local project:

```rust
fn main() {
    println!("This line is missing its closing punctuation"
}
```

Run `cargo check`. The compiler reports a syntax problem and points near the place where it can no longer parse the program. Read the first primary error, not every later message as a separate problem.

Repair it yourself before reading the corrected version:

```rust
fn main() {
    println!("This line is valid.");
}
```

The important skill is not memorizing the fix. Identify the rule the program violated and connect the diagnostic to that rule.

## Mental model

- Your source code is input to tools. It is not the executable itself.
- Cargo is the normal front door for building Rust projects.
- Generated files and source files have different roles.
- A repeatable command is better than an undocumented manual step.

## Common mistakes

- Typing commands from the wrong directory. Use `pwd` on macOS/Linux or `Get-Location` in PowerShell when unsure.
- Editing files under `target/`. Cargo can regenerate that directory.
- Installing random standalone Rust binaries instead of using rustup unless you have an environment-specific reason.
- Treating a failed command as proof the language is broken. Read the command, current directory, and first diagnostic.

## Transfer to other languages

Every serious language has some equivalent of a toolchain and project workflow: a compiler or interpreter, package/build tooling, source directories, and generated artifacts. The names differ, but the separation of source, tools, and outputs transfers directly.

The syntax may change in another language, but the underlying problem does not disappear.

## Guided practice

1. Run `rustc --version` and `cargo --version`.
2. Open `Cargo.toml` and identify the package name and edition.
3. Change the printed message, run `cargo check`, then `cargo run`.
4. Run `cargo fmt` and inspect whether the source changed.

## Independent exercise and quiz

Complete [the exercises](exercise/exercise.md), then [the quiz](quiz/quiz.md). Do both before opening the answer directories.

## Readiness check

You are ready to continue when you can:

- explain what rustup, rustc, Cargo, rustfmt, and Clippy are for;
- create a Rust 2024 Cargo project from a terminal;
- find `Cargo.toml`, `src/main.rs`, and `target/`;
- run `cargo check`, `cargo run`, and `cargo fmt`.

## Next

Continue to [Module 02](../02-first-program-and-compile-run-cycle/README.md).
