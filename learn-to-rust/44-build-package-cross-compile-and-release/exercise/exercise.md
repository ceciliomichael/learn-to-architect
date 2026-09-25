# Exercises: Module 44

## 1. Inspect a release artifact

Choose a previous binary project.

Run:

~~~text
cargo build --release --locked
~~~

Record:

- artifact path;
- file size;
- rustc -vV output;
- source commit if the project is in Git;
- enabled features;
- direct dependencies.

Run the artifact directly instead of using cargo run.

## 2. Cross-compilation plan

Choose one target platform different from your current host.

Do not install random toolchains yet.

Write CROSS_COMPILE_PLAN.md containing:

- host;
- desired target;
- Rust target requirement;
- linker requirement;
- native dependencies;
- SDK/system library needs;
- how the artifact will be tested on the real target.

Mark unknown details as unknown.

## 3. Package a CLI

Create a disposable release directory containing:

- release binary;
- short README;
- license notices required by your own project/dependencies;
- checksum file;
- placeholder SBOM directory or generated SBOM if tooling is available and reviewed.

Do not include source-control secrets or local config files.

## 4. Build a release checklist

Write RELEASE.md for the final capstone.

Include:

1. versioning;
2. source revision;
3. formatting;
4. linting;
5. tests;
6. dependency review;
7. locked build;
8. artifact smoke test;
9. package creation;
10. SBOM/checksum/signing policy;
11. release notes;
12. rollback.

## 5. Rollback analysis

Assume version 2 changes a JSON persistence format used by version 1.

Write a rollback strategy.

Do not say simply restore version 1.

Explain how stored data remains readable or how backup/migration strategy prevents an unusable rollback.
