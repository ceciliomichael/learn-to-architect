# Module 43: Dependency and Supply-Chain Security

## Outcome

By the end of this module, you can review a Rust dependency graph, distinguish direct and transitive risk, keep builds reproducible, evaluate third-party trust deliberately, and integrate dependency/security checks into normal development without treating automated tools as proof of safety.

## Why this matters

When your program depends on a crate, you are not only importing an API.

You are accepting code into your:

- build;
- binary;
- tests;
- build scripts;
- procedural macros;
- transitive graph;
- update process.

A package manager makes reuse practical.

It does not remove the need to decide what you trust.

## Programming concept

A **software supply chain** is the path through which source code, dependencies, build tools, generated artifacts, and releases reach users.

A **direct dependency** is one your package declares.

A **transitive dependency** is brought in by another dependency.

A **lock file** records one concrete dependency resolution.

An **advisory** reports a known vulnerability or security concern.

A **license** defines legal conditions for using and distributing code.

**Provenance** is evidence about where software or an artifact came from.

## Rust model

Cargo gives you strong visibility into your graph.

Built-in tools include:

~~~text
cargo tree
cargo metadata
cargo update
cargo fetch
~~~

Cargo.toml states dependency requirements.

Cargo.lock records the concrete resolution used by the project.

For application repositories, committing Cargo.lock is normally important for reproducible dependency resolution.

Rust's ecosystem also contains third-party auditing and policy tools.

Tool names, installation methods, advisory databases, and exact command options can change over time.

When using an external security tool, read its current authoritative documentation before putting it in CI.

The course will focus first on principles that remain valid regardless of the specific scanner.

## Inspect your graph

In a Cargo project, run:

~~~text
cargo tree
~~~

Look for:

- direct dependencies;
- repeated versions;
- large subgraphs;
- platform-specific packages;
- optional features;
- build dependencies.

To understand why one package exists, use Cargo's reverse-tree support.

For a package named example_dependency, conceptually:

~~~text
cargo tree -i example_dependency
~~~

This shows who depends on it.

That question matters when removing or updating a transitive package.

## Direct versus transitive trust

Suppose your Cargo.toml contains:

~~~toml
[dependencies]
framework = "1"
~~~

cargo tree might reveal dozens of packages.

Your real build includes the graph Cargo resolved, not only the names you typed.

That does not mean a large graph is automatically bad.

It means review scope is larger.

Useful questions include:

- Which package introduced this dependency?
- Is it used only on one platform?
- Is it activated by an unnecessary feature?
- Does another dependency already provide the needed capability?
- Is the dependency maintained?
- Does it contain unsafe code?
- Does it execute a build script?
- Does it use a procedural macro?
- What licenses apply?
- What known advisories affect the resolved versions?

## Cargo.lock

Cargo.toml expresses requirements such as:

~~~toml
serde = "1"
~~~

Cargo.lock records the concrete selected versions for the full graph.

That gives an application team a specific dependency set to:

- test;
- review;
- scan;
- reproduce;
- update deliberately.

Deleting Cargo.lock every build would make dependency selection less predictable.

## Library versus application lock files

For applications and binaries, commit Cargo.lock.

For published libraries, Cargo consumers resolve your library within their own larger dependency graph.

Even so, a library repository may keep a lock file for testing and development consistency depending on project policy and Cargo behavior.

The key principle is to understand who owns final dependency resolution for the shipped artifact.

Do not cargo-cult lock-file rules from another ecosystem.

## Updates should be deliberate

A dependency update is code change.

Even when your own source files do not change, the resulting program can.

A disciplined update process is:

1. inspect what will change;
2. update a bounded set of packages when practical;
3. review the lock-file diff;
4. run tests;
5. run Clippy and checks;
6. run security/policy scans;
7. exercise important runtime paths;
8. record notable behavior or migration changes.

Avoid a process where every build silently floats to unreviewed new versions.

## Minimum dependency policy

A useful default is:

**Do not add a dependency without a reason.**

But do not interpret that as:

**Reimplement everything yourself.**

Complex areas such as:

- TLS;
- cryptography;
- HTTP;
- Unicode;
- serialization;
- async runtime;
- compression;
- database protocols;

often benefit from mature maintained implementations.

The security question is not dependency versus no dependency.

It is:

**Which implementation reduces total risk for this requirement?**

## Evaluate a crate

Before adopting an important crate, review:

### Purpose

What exact requirement does it solve?

### API fit

Are you using a small stable part of the API or coupling your architecture deeply to it?

### Maintenance

Look for current project activity, release cadence appropriate to the project, issue handling, and supported Rust/toolchain policy.

Do not reduce maintenance quality to one metric.

### Ownership and governance

Understand who maintains the project and where releases come from.

### Documentation

Can you understand the safety, error, and compatibility contracts?

### Transitive graph

Run Cargo graph inspection.

### Feature surface

Disable unnecessary optional features where supported.

### Unsafe code

Unsafe is not automatically bad.

Low-level crates may require it.

The question is whether unsafe boundaries are justified, reviewed, tested, and maintained.

### Build scripts and procedural macros

These execute code during build or compilation.

Treat them as part of the trusted toolchain surface.

### License

Confirm that the license terms are compatible with how your organization uses and distributes the software.

### Advisories

Check the resolved dependency set against current security advisories using maintained tooling and authoritative advisory sources.

## Automated scanners are evidence

A clean vulnerability scan does not prove a dependency is secure.

A scanner generally knows about:

- published advisories;
- policy rules;
- metadata.

It may not know about:

- undisclosed vulnerabilities;
- malicious new releases;
- logic flaws in your use of the library;
- unsafe application configuration;
- compromised credentials;
- architectural trust mistakes.

Treat scanning as one layer.

## Build scripts

Cargo packages can contain build.rs.

A build script may:

- detect system libraries;
- generate bindings;
- compile native code;
- emit linker configuration;
- generate source.

It also executes during the build.

Review unexpected build scripts in sensitive dependency chains.

## Procedural macros

Procedural macros run at compile time.

They are powerful because they transform Rust syntax.

They also become executable build-time dependencies.

This does not mean avoid them entirely.

It means include them in your trust model.

## Secrets do not belong in source control

Never intentionally commit:

- API tokens;
- private keys;
- passwords;
- cloud credentials;
- signing secrets.

Use your deployment environment's secret-management mechanism.

Also review:

- generated config;
- example files;
- shell history;
- CI logs;
- build output;
- diagnostic logs.

A secret can leak outside source files.

## CI dependency access

Build pipelines need the minimum credentials and permissions required.

Avoid giving dependency or release jobs broad write credentials when they only need read access.

Separate:

- build;
- test;
- package;
- sign;
- publish;

when the trust model benefits from separation.

## Reproducibility

A reproducible build process aims to make the same source and dependency inputs produce predictable artifacts.

Perfect byte-for-byte reproducibility can require control over:

- compiler version;
- target toolchain;
- linker;
- native libraries;
- environment;
- timestamps;
- build scripts.

Even when full reproducibility is not achieved, pinning toolchain and dependency inputs improves traceability.

## Toolchain pinning

A project can record an expected Rust toolchain with rust-toolchain.toml when appropriate.

For example:

~~~toml
[toolchain]
channel = "stable"
components = ["rustfmt", "clippy"]
~~~

A production project may choose a specific supported Rust version instead of floating stable if reproducibility requirements demand it.

That is a project policy decision.

## Deliberate mistake

Imagine this process:

~~~text
cargo update
cargo build --release
publish immediately
~~~

with no review, tests, or graph inspection.

A safer process is:

~~~text
inspect update
    |
    v
review lock diff
    |
    v
check + test + clippy
    |
    v
security / license policy checks
    |
    v
runtime validation
    |
    v
release
~~~

Automation should make this easier and more repeatable.

## Dependency removal is security work too

Removing an unused dependency can reduce:

- build time;
- transitive graph;
- advisory surface;
- licenses to track;
- build scripts;
- procedural macros;
- future update workload.

Before removal, verify the package is genuinely unused across feature and target combinations.

## Software Bill of Materials

An **SBOM** is an inventory of software components included in a product or build.

It can help with:

- vulnerability response;
- license review;
- customer requirements;
- incident investigation;
- identifying whether a vulnerable component is present.

Common SBOM ecosystems include standardized formats such as SPDX and CycloneDX.

The exact generator/tooling you use should match your organization's requirements and current tool support.

An SBOM is not a vulnerability scan.

It answers a different question:

**What is in this software?**

## Threat model your dependency process

Ask:

- Who can change Cargo.toml?
- Who can approve lock-file changes?
- Who can publish internal crates?
- Which registries are trusted?
- Can CI download arbitrary network content?
- Who owns release credentials?
- What happens if a dependency is yanked or compromised?
- How quickly can you identify affected products?

Supply-chain security includes process, not only code.

## Mental model

- Dependencies are code you trust.
- Review the whole resolved graph, not only direct names.
- Commit and review lock-file changes for shipped applications.
- Updates are code changes.
- Minimize dependencies without reimplementing expert-level protocols recklessly.
- Build scripts and procedural macros are part of the trust surface.
- Automated scanners provide evidence, not proof.
- Keep secrets out of source, artifacts, and logs.
- Know what is in your product.
- Make dependency review repeatable.

## Common mistakes

### Download count equals trust

Popularity is one signal, not proof.

### Zero dependencies as a security goal

Reimplementing cryptography or protocol stacks can create greater risk.

### Ignoring transitive dependencies

They execute in your build or product too.

### Running scanners but never reviewing results

A check that everyone ignores is not a control.

### Updating everything immediately before release

This expands the change surface at the riskiest time.

### Assuming Cargo.lock makes the build completely reproducible

It fixes Rust dependency resolution, not every compiler, linker, native library, build-script, and environment input.

## Transfer to other languages

The same concerns appear in:

- npm lock files;
- Python requirements and lock tools;
- Maven/Gradle dependency graphs;
- NuGet;
- Go modules;
- container images;
- operating-system packages.

Supply-chain security is ecosystem-independent.

## Guided practice

1. Run cargo tree on a checkpoint project.
2. Pick one transitive package and find why it exists.
3. Review enabled features on one major dependency.
4. Read the lock-file diff after a controlled update in a disposable branch.
5. List build dependencies and procedural macros in the graph.
6. Write a one-page dependency review for one external crate.
7. Create an SBOM plan for your final capstone.
8. Identify where release secrets would be stored outside source control.

## Exercise and quiz

Complete the exercises and quiz before opening the answers.

- [Exercises](exercise/exercise.md)
- [Quiz](quiz/quiz.md)

## Readiness check

You are ready to continue when you can:

- distinguish direct and transitive dependencies;
- explain Cargo.toml versus Cargo.lock;
- inspect why a package exists;
- review an update as code change;
- evaluate features and build-time execution;
- explain what an SBOM is;
- keep secrets outside source control;
- describe why a clean scanner result is not proof of security.

## Next

Continue to [Module 44](../44-build-package-cross-compile-and-release/README.md).
