# Exercise: Create a two-package workspace

1. Make a workspace with `core` as a library and `app` as a binary.
2. Set `resolver = "3"` in the root `Cargo.toml`.
3. Give `core` a `friendly` feature with no dependencies and no default features.
4. Compile a different `greeting()` result when `friendly` is enabled.
5. Make `app` call `core::greeting()`. Test once without the feature and once with it.
