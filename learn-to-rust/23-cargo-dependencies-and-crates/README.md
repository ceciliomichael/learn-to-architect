# Module 23: Cargo Dependencies and the Crate Ecosystem

## Outcome

Add and inspect external crates responsibly, understand Cargo.toml and Cargo.lock, use crate documentation, reason about versions and features, and evaluate dependency cost and trust.

## Why this matters

Real applications should not reimplement every JSON parser, TLS stack, async runtime, CLI parser, or Unicode algorithm. Reuse is essential, but every dependency adds code, transitive dependencies, maintenance assumptions, licenses, security exposure, and build complexity.

## Programming concept

A package ecosystem distributes reusable components. A dependency graph contains direct dependencies you choose and transitive dependencies they choose. Version requirements constrain acceptable releases; a lock file records one resolved graph for reproducibility.

## Rust model

Cargo reads dependency requirements from Cargo.toml and records concrete resolutions in Cargo.lock. cargo add edits dependencies safely, cargo remove removes direct dependencies, cargo tree shows the graph, and feature flags activate optional capabilities. crates.io is Rust's primary public registry. Applications should normally commit Cargo.lock so a reviewed resolution can be reproduced.

## Local Cargo example

Create cargo new grapheme_counter --edition 2024, enter it, run cargo add unicode-segmentation, then inspect Cargo.toml and Cargo.lock before replacing src/main.rs.

~~~rust
use unicode_segmentation::UnicodeSegmentation;

fn main() {
    let text = "a̐éö̲";

    println!("bytes: {}", text.len());
    println!("chars: {}", text.chars().count());
    println!("graphemes: {}", text.graphemes(true).count());
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- The dependency solves a specific Unicode grapheme-cluster problem rather than duplicating a trivial helper.
- cargo add records an appropriate dependency requirement.
- Cargo.lock records the concrete resolved graph.
- The imported extension trait provides graphemes on string slices.
- Adoption still requires review of documentation, maintenance, licenses, features, dependency graph, and security posture.

## Deliberate mistake

~~~rust
# Anti-pattern idea in Cargo.toml:
[dependencies]
some-huge-crate = "*"

~~~

An unrestricted requirement and unreviewed crate make the version and trust boundary vague. Package-manager convenience is not a substitute for dependency judgment.

Corrected direction:

~~~rust
# Prefer a deliberate workflow:
# cargo add package-name
# cargo tree
# inspect Cargo.toml and Cargo.lock
# read authoritative crate documentation
# enable only needed features

~~~

## Mental model

- A dependency is code your project chooses to trust and maintain through upgrades.
- Cargo.toml states requirements; Cargo.lock records one resolution.
- One direct dependency can bring many transitive packages.
- Features should enable needed capabilities, not everything by default.
- Read current documentation for the version you use instead of copying random snippets.
- Use the standard library when it solves the problem well; use a crate when reuse meaningfully reduces work or risk.

## Common mistakes

- Adding a crate for a trivial helper.
- Enabling all features by default.
- Deleting Cargo.lock from an application without understanding reproducibility.
- Judging quality only by popularity.
- Copying outdated blog examples instead of current docs.
- Assuming Rust code cannot contain logic, security, unsafe, or supply-chain risks.

## Transfer to other languages

npm, PyPI, Maven, NuGet, Go modules, and other ecosystems have the same graph, version, licensing, maintenance, and trust concerns. Package managers automate mechanics; they do not make architecture decisions.

## Guided practice

1. Run cargo tree and identify direct versus transitive packages.
2. Explain Cargo.toml versus Cargo.lock from your project.
3. Use cargo remove and observe graph changes.
4. Inspect enabled features for a dependency.
5. Use cargo metadata --format-version 1 and recognize the dependency model is machine-readable.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- add and remove crates with Cargo;
- explain manifest versus lock file;
- identify transitive dependencies;
- explain feature flags;
- list purpose, maintenance, license, security, API, and graph questions before adopting a crate.

## Next

Continue to [Checkpoint Project C](../projects/project-c-multi-module-cli/README.md).
