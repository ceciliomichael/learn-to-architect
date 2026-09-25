# Module 44: Build, Package, Cross-Compile, and Release

## Outcome

By the end of this module, you can produce release artifacts deliberately, distinguish build targets from host systems, reason about cross-compilation limits, verify packaged artifacts, attach version/provenance information, and design a release process with rollback rather than treating cargo build --release as the entire delivery story.

## Why this matters

A program that works on your development machine is not yet a release.

Users receive artifacts built for a target environment.

That process must answer:

- Which source revision was built?
- Which dependency graph was used?
- Which Rust toolchain was used?
- Which target was built?
- Which features were enabled?
- Which artifact should users run?
- How is integrity checked?
- How do we know the artifact starts and behaves correctly?
- How do we roll back a bad release?

Release engineering connects source code to deployed software.

## Programming concept

A **build artifact** is an output produced from source and dependencies.

A **target** describes the environment the artifact is built to run on.

A **host** is the environment performing the build.

**Cross-compilation** means building on one host for a different target.

**Packaging** prepares artifacts and metadata for distribution.

**Provenance** records where an artifact came from.

**Rollback** restores a known-good version after a bad deployment.

## Rust model

Cargo supports optimized release builds:

~~~text
cargo build --release
~~~

For a binary package, the output normally appears under:

~~~text
target/release/
~~~

depending on target and configuration.

Build exactly the configuration you intend to ship.

For a workspace:

~~~text
cargo build --workspace --release
~~~

For one package:

~~~text
cargo build -p app --release
~~~

With features:

~~~text
cargo build -p app --release --features feature-name
~~~

For reproducible dependency resolution in an application release, use the committed lock file and prevent Cargo from updating it during the build:

~~~text
cargo build --release --locked
~~~

## Start with a release build

Use one previous project.

Run:

~~~text
cargo fmt --check
cargo clippy --all-targets --all-features
cargo test --all-features
cargo build --release --locked
~~~

Adjust all-features if your supported feature matrix requires separate combinations rather than one unified build.

A release pipeline should build only after verification succeeds.

## Debug and release are different artifacts

Do not test only:

~~~text
cargo run
~~~

and assume:

~~~text
cargo build --release
~~~

must behave identically in every edge case.

Optimization can expose:

- timing assumptions;
- undefined behavior in unsafe code;
- race conditions;
- reliance on debug assertions;
- overflow differences when code did not define arithmetic intentionally.

Run important tests and smoke tests against the release configuration too.

## Host and target triples

Rust target names encode platform information.

A target triple may describe:

- CPU architecture;
- vendor or platform;
- operating system;
- ABI/environment.

Examples vary by platform.

Do not memorize a list from a tutorial.

Inspect the toolchain installed on your machine:

~~~text
rustc --version
rustc -vV
rustup target list --installed
~~~

Use current toolchain output as the source of truth for the environment you are building.

## Installing another Rust target

Conceptually:

~~~text
rustup target add TARGET
cargo build --release --target TARGET
~~~

Adding a Rust target is only part of cross-compilation.

A project may also require:

- a linker for the target;
- target C runtime;
- native libraries;
- platform SDK;
- C compiler;
- pkg-config metadata;
- system headers.

Pure-Rust dependencies can make cross-compilation easier, but do not assume every crate graph is pure Rust.

## Cross-compilation is a dependency problem too

Suppose a crate uses:

- OpenSSL from the system;
- SQLite C library;
- a C compiler through build.rs;
- bindgen;
- platform-specific SDK APIs.

Installing the Rust standard library for another target does not automatically provide those external components.

Inspect:

~~~text
cargo tree
~~~

and your build logs.

Know which packages compile native code.

## Build for the actual target

The most reliable validation happens on the target environment or something meaningfully equivalent.

A cross-compiled binary that links successfully can still fail because of:

- missing runtime library;
- incompatible CPU features;
- unavailable filesystem paths;
- certificate store differences;
- permission model;
- environment assumptions;
- platform-specific behavior.

Compilation is one gate.

Execution is another.

## Packaging a CLI application

A simple release package might contain:

~~~text
myapp/
  myapp.exe or myapp
  README.txt
  LICENSES/
  SBOM/
  checksums.txt
~~~

Your actual product may instead use:

- installer;
- package manager;
- container image;
- mobile package;
- embedded firmware;
- system service package.

Packaging format follows the deployment environment.

Do not invent a custom installer when the target ecosystem already has a standard mechanism.

## Version information

Users and operators need to identify a running build.

A CLI can expose:

~~~text
myapp --version
~~~

Useful version metadata may include:

- semantic version;
- source commit;
- build date when reproducibility policy permits;
- build profile;
- target;
- feature set.

Be careful with timestamps if byte-for-byte reproducibility matters.

A source commit identifier is often more useful than a vague build label.

## Build-time metadata

A build script or CI environment can inject metadata.

Do not make core functionality depend on an unavailable CI variable without a fallback.

Keep generated metadata:

- deterministic where required;
- non-secret;
- short;
- clearly documented.

Never embed signing secrets or CI credentials into the binary.

## Checksums

A cryptographic checksum lets a user verify that downloaded bytes match the published artifact bytes.

For each release artifact, generate a checksum using a standard cryptographic hash available in your release environment.

A checksum provides integrity comparison.

It does not by itself prove who published the artifact.

Authenticity requires a trusted distribution/signing mechanism.

## Signing

Some products sign:

- binaries;
- packages;
- containers;
- release manifests.

Signing systems vary by platform and organization.

Signing keys are high-value secrets.

Protect them with:

- limited access;
- secure storage;
- audited release workflows;
- separation from ordinary build credentials.

Do not place private signing keys in the repository.

## Artifact provenance

A release should be traceable back to its inputs.

Record enough information to answer:

~~~text
Which source revision produced this artifact?
Which dependency lock file?
Which toolchain?
Which build command?
Which target?
Which features?
Which CI workflow or environment?
~~~

An SBOM complements this by describing included components.

## Smoke testing the artifact

Do not stop after the compiler exits successfully.

A smoke test is a small high-value verification against the built artifact.

For a CLI:

~~~text
myapp --version
myapp --help
myapp doctor
~~~

or another harmless command.

For a service:

- start it;
- wait for readiness;
- call a health endpoint;
- perform one representative request;
- shut it down cleanly.

Smoke tests should exercise the packaged artifact, not silently rebuild from source.

## Release notes

Release notes should tell users what changed in language they can act on.

Useful categories may include:

- features;
- bug fixes;
- compatibility changes;
- migrations;
- security changes;
- known issues.

Do not copy raw commit messages as a substitute for release communication unless those messages were intentionally written for users.

## Rollback is part of release design

Before deployment ask:

- Can the previous artifact be restored?
- Are database or file-format migrations backward compatible?
- Does the new version mutate data in a way the old version cannot read?
- Can configuration be rolled back?
- Are old artifacts retained?
- How is rollback triggered?
- What state may be lost?

A binary rollback is easy only when surrounding state remains compatible.

## Data migration risk

Application version:

~~~text
v2
~~~

may write a new storage format.

If rollback to v1 is required, ask whether v1 can read that format.

Possible strategies include:

- backward-compatible schema changes;
- staged migrations;
- dual-read transition;
- backup before destructive migration;
- forward-fix instead of rollback.

Release engineering includes data compatibility.

## CI pipeline shape

A simple conceptual pipeline:

~~~text
source checkout
      |
      v
format check
      |
      v
clippy
      |
      v
tests
      |
      v
dependency/security policy
      |
      v
release build
      |
      v
artifact smoke test
      |
      v
package
      |
      v
SBOM/checksum/signing
      |
      v
publish
~~~

Not every project needs separate infrastructure for every box.

The ordering matters because publishing should happen only after verification.

## Deliberate mistake

Bad release process:

~~~text
developer laptop
      |
      v
cargo build --release
      |
      v
upload target/release/app
~~~

No record of:

- source commit;
- lock file;
- toolchain;
- target;
- tests;
- checksum;
- dependency review;
- release notes;
- rollback.

A repeatable release command or CI workflow is safer because the process becomes reviewable.

## Containers are not magic portability

A container can package userspace dependencies consistently.

It does not remove:

- CPU architecture;
- kernel behavior;
- filesystem;
- networking;
- permissions;
- secrets;
- host resource limits;
- image supply chain.

Containers are one packaging mechanism.

## Libraries release differently

A library release may publish source/package metadata to a registry instead of a binary.

Library release work includes:

- public API compatibility;
- package contents;
- documentation;
- feature combinations;
- minimum supported Rust policy;
- license files;
- dependency requirements.

Use the registry's packaging inspection tools before publishing.

Do not publish from the learning repository during this course.

## Release checklist

Before release:

~~~text
[ ] clean intended source revision
[ ] version updated intentionally
[ ] lock file reviewed
[ ] formatting passes
[ ] Clippy passes
[ ] tests pass
[ ] supported feature combinations pass
[ ] dependency/security review passes
[ ] release build succeeds with locked dependencies
[ ] packaged artifact smoke-tested
[ ] version/provenance identifiable
[ ] SBOM generated if required
[ ] checksums/signatures generated if required
[ ] release notes prepared
[ ] rollback plan understood
[ ] publishing credentials scoped and protected
~~~

Adapt the checklist to the project.

## Mental model

- Build output is not automatically a release.
- Host and target are separate concepts.
- Cross-compilation includes native/toolchain dependencies.
- Test the release configuration.
- Package the artifact for the target ecosystem.
- Make versions traceable to source and dependencies.
- Checksums verify bytes; signing can establish authenticity through a trust system.
- Smoke-test the artifact you will ship.
- Plan rollback before deployment.
- Protect release credentials.
- Make release steps repeatable.

## Common mistakes

### Testing source but not the packaged artifact

Packaging can omit files or alter runtime environment.

### Floating dependency resolution during release

Use the reviewed lock file for application release builds.

### Cross-compiling without a target linker

Rust target installation is not the full native toolchain.

### Rollback with irreversible data changes

A previous binary may not understand new state.

### Publishing from an unclean workstation manually

Manual release paths are harder to reproduce and audit.

### Embedding secrets as build metadata

Anything in a binary or package should be assumed discoverable.

## Transfer to other languages

All ecosystems need:

- build artifacts;
- dependency resolution;
- target environments;
- packaging;
- signing;
- versioning;
- release notes;
- rollback.

The commands differ.

The release discipline does not.

## Guided practice

1. Build a previous project with --release and --locked.
2. Inspect rustc -vV.
3. Inspect installed targets.
4. Identify native dependencies in cargo tree.
5. Run the release binary directly from target.
6. Add a --version path if the application lacks one.
7. Create a checksum for a disposable artifact using your platform's standard tool.
8. Write a release checklist.
9. Write a rollback note for the persistent CLI checkpoint.

## Exercise and quiz

Complete the exercises and quiz before opening the answers.

- [Exercises](exercise/exercise.md)
- [Quiz](quiz/quiz.md)

## Readiness check

You are ready to continue when you can:

- build a locked release artifact;
- explain host versus target;
- identify cross-compilation dependencies beyond Rust;
- package a binary deliberately;
- trace an artifact to source and dependency inputs;
- explain checksum versus signing;
- smoke-test the shipped artifact;
- describe rollback risks;
- design a repeatable release pipeline.

## Next

Continue to [Module 45](../45-reading-real-rust-and-learning-next-language/README.md).
