# Module 37: Dependency and Supply-Chain Security

Every dependency adds code, maintainers, build behavior, and future updates to the program's trust boundary. Add one when it provides enough value to justify that cost.

Before adding a crate, inspect its repository, maintenance activity, ownership, license, documentation, release history, feature defaults, transitive dependencies, and security record. A short name or high download count is not proof of trust.

Useful Cargo commands include:

```text
cargo tree
cargo tree -e features
cargo metadata --format-version 1
```

Install maintained auditing tools through your organization's reviewed tool process, then run advisory and license checks in continuous integration. Tool names and policies change, so document the exact approved tools and versions rather than treating one command as permanent security.

Build scripts and procedural macros execute code during a build. Review them with the same care as runtime code. Disable unused default features, keep the graph small, and never place secrets in source, Cargo configuration committed to the repository, or build logs.

Commit and review lock-file changes for applications. Update in small groups, read release notes, run tests on supported targets, and keep a rollback path. Reproducibility also requires controlling the Rust toolchain, target, system libraries, and build environment.

Security is ongoing maintenance. An approved dependency can later change ownership, become unmaintained, or receive an advisory.

Continue to [Module 38](../38-build-package-and-release/README.md).
