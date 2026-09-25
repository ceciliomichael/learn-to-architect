# Module 39: Cargo Features and Workspaces

## Outcome

By the end of this module, you can split a larger Rust codebase into multiple packages, share workspace configuration, use feature flags for optional capabilities, and avoid feature designs that create fragile combinations.

## Why this matters

A project can begin as one package and still be well designed. As responsibilities grow, however, you may eventually want independently reusable libraries, clearer dependency direction, smaller build boundaries, or optional capabilities that not every consumer needs.

Cargo workspaces and features solve those problems when they represent real architecture. They are not a requirement for every project.

## Programming concept

A **workspace** groups related packages under one repository and build graph.

A **dependency graph** shows which packages depend on which others.

A **feature flag** enables an optional compile-time capability.

Good modularity should make responsibilities and dependency direction easier to understand. Bad modularity merely spreads one tightly coupled program across more files and packages.

## Rust model

Cargo workspaces are declared in a root Cargo.toml with a workspace table.

A workspace can:

- contain multiple packages;
- run commands across all members;
- share dependency version requirements;
- share package metadata;
- use one Cargo.lock for the workspace;
- coordinate feature resolution.

For Rust 2024 workspaces, use Cargo feature resolver version 3 unless you have a specific compatibility reason not to.

Features are declared in a package Cargo.toml. They are compile-time capabilities. Optional dependencies can be activated by features.

Cargo generally **unifies features** requested for the same resolved dependency. This is why normal features should be designed to be additive whenever practical.

## Build a real workspace

Create a new directory outside another Cargo package:

~~~text
mkdir workspace_demo
cd workspace_demo
cargo new crates/domain --lib --edition 2024
cargo new crates/cli --bin --edition 2024
~~~

Create this root Cargo.toml:

~~~toml
[workspace]
resolver = "3"
members = [
    "crates/domain",
    "crates/cli",
]

[workspace.package]
edition = "2024"

[workspace.dependencies]
serde = { version = "1", features = ["derive"] }
~~~

Now the directory conceptually looks like:

~~~text
workspace_demo/
  Cargo.toml
  crates/
    domain/
      Cargo.toml
      src/lib.rs
    cli/
      Cargo.toml
      src/main.rs
~~~

Run:

~~~text
cargo check --workspace
~~~

Cargo now treats the member packages as one workspace while they remain separate Rust packages and crates.

## Package dependency direction

Suppose the CLI should depend on the domain library.

In crates/cli/Cargo.toml:

~~~toml
[dependencies]
domain = { path = "../domain" }
~~~

The dependency direction is:

~~~text
cli
 |
 v
domain
~~~

The domain crate does not need to know that a command-line application exists.

That asymmetry is useful. Domain rules can later be reused by another binary, service, desktop application, or test harness without importing CLI dependencies.

## Workspace dependencies

A workspace-level dependency declaration does not automatically make every member depend on that crate.

For example, the root may contain:

~~~toml
[workspace.dependencies]
serde = { version = "1", features = ["derive"] }
~~~

A member that actually needs Serde can opt into the workspace requirement:

~~~toml
[dependencies]
serde = { workspace = true }
~~~

This centralizes version requirements without pretending every member needs the dependency.

## Optional dependencies and features

Now imagine the domain package has an optional serialization capability.

In crates/domain/Cargo.toml:

~~~toml
[features]
default = []
serde-support = ["dep:serde"]

[dependencies]
serde = { workspace = true, optional = true }
~~~

A consumer can enable it:

~~~toml
[dependencies]
domain = { path = "../domain", features = ["serde-support"] }
~~~

Or from the command line:

~~~text
cargo check -p domain --features serde-support
~~~

The package still builds without the optional capability:

~~~text
cargo check -p domain --no-default-features
~~~

## Features should usually be additive

This design is fragile:

~~~toml
[features]
fast = []
slow = []
~~~

if application code assumes **exactly one** of fast or slow is enabled.

Another package in the graph may request fast while a different package requests slow. Cargo may then build the dependency with both enabled.

A safer feature design is usually:

~~~toml
[features]
default = []
json = ["dep:serde_json"]
metrics = ["dep:metrics"]
compression = ["dep:flate2"]
~~~

Each feature adds a capability.

If the program needs to choose exactly one operational strategy, that may be better represented as:

- runtime configuration;
- separate concrete types;
- separate packages;
- an enum;
- a constructor choice.

Do not force every mode decision into Cargo features.

## Default features

Default features are enabled unless a consumer disables them.

Keep defaults small and unsurprising.

A library whose default feature set pulls in a large runtime, TLS implementation, database driver, or platform integration should have a clear reason.

Test the minimal configuration when your package claims to support it:

~~~text
cargo check -p domain --no-default-features
~~~

Test the combined supported feature set:

~~~text
cargo check -p domain --all-features
~~~

If many independent features exist, all-features is not enough to prove every meaningful combination. Test combinations that matter to your supported contract.

## Workspace commands

Useful commands include:

~~~text
cargo check --workspace
cargo test --workspace
cargo clippy --workspace --all-targets
cargo fmt --all --check
cargo tree
cargo tree -p cli
cargo check -p domain
~~~

The -p option selects one package.

## Deliberate mistake

Imagine this workspace:

~~~text
cli -> domain
domain -> cli
~~~

This circular dependency is not a clean layering strategy. Each package needs the other to build.

Even when a tool prevents a direct cycle, code can still create conceptual cycles by moving shared abstractions into the wrong layer.

A better direction is:

~~~text
cli
 |
 v
domain
~~~

If both need a genuinely shared lower-level concept, extract that concept only when it represents a real independent responsibility:

~~~text
cli --------\
             v
          shared-core
             ^
domain ------/
~~~

Do not extract a third crate merely to silence a design problem. First ask whether the dependency direction itself is wrong.

## Mental model

- A module organizes names inside a crate.
- A crate is one Rust compilation unit.
- A package contains Cargo-managed crate targets.
- A workspace coordinates multiple packages.
- Create package boundaries for meaningful responsibilities.
- Features should normally add capabilities.
- Workspace dependency declarations centralize requirements but do not force every member to use them.
- Keep lower-level domain code independent from higher-level delivery mechanisms where practical.
- Test the feature sets you claim to support.

## Common mistakes

### One crate per folder

More crates are not automatically more architecture.

Each crate adds:

- manifest maintenance;
- public API boundaries;
- compilation boundaries;
- dependency decisions;
- versioning considerations if published;
- navigation cost.

### Features as ordinary configuration

Do not make users recompile the program merely to select a log level, server address, theme, or environment.

Those are normally runtime configuration.

### Mutually exclusive features

Ordinary Cargo features can be combined by dependency resolution.

Designing invalid combinations creates surprises for downstream consumers.

### Every dependency in workspace.dependencies

Centralize dependencies that are genuinely shared. A giant root list can make ownership less clear if only one member ever uses most entries.

### Only testing the default build

Optional code paths can rot.

If a feature is supported, include it in your verification strategy.

## Transfer to other languages

Workspaces are conceptually related to:

- npm or pnpm workspaces;
- Maven multi-module builds;
- Gradle projects;
- .NET solutions;
- Go multi-module repositories;
- Bazel package graphs.

Feature flags are related to optional build dependencies and compile-time capabilities in many ecosystems.

The transferable ideas are:

- dependency direction;
- modular build boundaries;
- optional capabilities;
- avoiding cycles;
- keeping configuration at the correct stage.

## Guided practice

1. Create a workspace containing two packages.
2. Make one package depend on the other through a path dependency.
3. Run cargo check --workspace.
4. Add one optional dependency behind a feature.
5. Verify the member builds without default features.
6. Verify it builds with the optional feature.
7. Draw the dependency graph in plain text.
8. Explain why every dependency arrow points in its current direction.

## Exercise and quiz

Complete the exercises and quiz before opening their answer files.

- [Exercises](exercise/exercise.md)
- [Quiz](quiz/quiz.md)

## Readiness check

You are ready to continue when you can:

- distinguish module, crate, package, and workspace;
- create a multi-package Cargo workspace;
- define a path dependency between members;
- share a dependency requirement through workspace configuration;
- make an external dependency optional;
- enable it through an additive feature;
- explain why mutually exclusive ordinary features are fragile;
- test supported feature combinations.

## Next

Continue to [Module 40](../40-api-design-documentation-and-compatibility/README.md).
