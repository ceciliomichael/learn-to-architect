# Module 38: Build, Package, and Release Rust Programs

A release is more than a successful compilation. It is a tested, identifiable artifact with a known source, toolchain, target, dependency graph, and rollback plan.

Start with repeatable checks:

```text
cargo fmt --check
cargo clippy --all-targets --all-features -- -D warnings
cargo test --all-features
cargo build --release --locked
```

`--locked` prevents Cargo from silently changing the lock file during an application release. Inspect the artifact in `target/release`, run it in an environment like production, and verify configuration, permissions, startup, shutdown, and failure behavior.

A target triple identifies architecture, vendor, operating system, and environment. Adding a target does not guarantee successful cross-compilation because native libraries and linkers may also be required. Test on every supported target.

Package only necessary files. Do not include secrets, local configuration, private keys, debug dumps, or unrelated build output. Record version, commit, compiler, checksums, dependency lock file, build command, and target. Sign artifacts when the delivery system supports a reviewed signing process.

Libraries should run `cargo package` and inspect the generated package before publishing. Publishing is an external, usually irreversible action and requires explicit authorization. This course does not publish anything.

Monitor the rollout, retain the previous known-good artifact, and write the rollback steps before deployment begins.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

You have now completed the planned Rust learning path. There is intentionally no miscellaneous module or final assessment.
