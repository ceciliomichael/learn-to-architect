# Exercises: Module 43

## 1. Trace a dependency

Choose one direct dependency from a previous checkpoint.

Run:

~~~text
cargo tree
~~~

Identify:

- the direct dependency;
- at least three transitive dependencies if present;
- one feature-enabled branch if visible;
- whether build dependencies appear.

Then use reverse dependency inspection on one transitive package and explain why it exists.

## 2. Review an update

On a disposable branch:

1. record cargo tree;
2. make one controlled dependency update;
3. inspect Cargo.lock;
4. run tests;
5. run Clippy;
6. inspect the new graph.

Write UPDATE_REVIEW.md describing what changed.

Do not publish anything.

## 3. Dependency adoption review

Pick a crate you might realistically use.

Write DEPENDENCY_REVIEW.md containing:

- exact requirement;
- why standard library is insufficient;
- API surface used;
- features needed;
- transitive graph summary;
- build scripts or procedural macros;
- license information you can actually verify;
- maintenance questions;
- security/advisory process;
- removal strategy.

If a fact is unknown, write unknown. Do not guess.

## 4. SBOM plan

For your final capstone, write SBOM_PLAN.md.

Include:

- which artifact the SBOM describes;
- direct and transitive Rust dependencies;
- native/system dependencies if any;
- toolchain information;
- chosen standard format;
- when it is generated;
- where it is stored with release artifacts;
- how you would use it during a vulnerability incident.

You do not need to install an SBOM generator yet.
