# Module 34: Cargo Features and Workspaces

A Cargo feature enables optional compile-time behavior. Features are additive: if any dependency path enables one, it is enabled for the build. Do not use features for mutually exclusive choices or to hide security fixes.

```toml
[features]
default = []
json = ["dep:serde_json"]

[dependencies]
serde_json = { version = "1", optional = true }
```

Code can use `#[cfg(feature = "json")]`. Test important feature combinations, including no default features and all features. A feature name becomes part of the public package contract.

A workspace groups related packages under one root:

```toml
[workspace]
members = ["app", "core"]
resolver = "3"
```

The Rust 2024 edition uses resolver version 3 by default for new edition-aware workspaces, but writing it explicitly makes the workspace intent visible. Workspace dependencies and shared package fields reduce repeated configuration while every member remains a separate package.

Commit `Cargo.lock` for applications and command-line tools so builds select reviewed versions. Libraries commonly omit it from published source because their users resolve the combined dependency graph, although keeping a lock file in the repository can still support local testing.

Profiles tune compilation. Release settings should be based on measurements and deployment needs, not copied blindly. Keep the workspace dependency graph understandable and avoid circular design between crates.

Continue to [Module 35](../35-documentation-api-design-and-compatibility/README.md).
