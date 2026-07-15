# Exercise: Write a dependency review

Choose one dependency already used by a practice Cargo project.

1. Record why the project needs it and whether the standard library is sufficient.
2. Record its source repository, license, current selected version, enabled features, and direct maintainer evidence.
3. Use `cargo tree -e features` to identify enabled and transitive features.
4. Note whether it has a build script or procedural macro.
5. Write an update and rollback plan. Do not include credentials or private registry tokens.
