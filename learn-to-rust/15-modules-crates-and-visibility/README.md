# Module 15: Modules, Crates, Packages, and Visibility

## What you will learn

You will split one Cargo package into focused crates and modules with a small public API.

A package is described by `Cargo.toml`. It can contain one library crate and several binary crates. A crate is one compilation unit. Modules organize paths inside a crate.

```rust
pub mod price {
    pub fn subtotal(cents: u32, quantity: u32) -> u32 {
        cents * quantity
    }
}
```

Items are private by default. `pub` exposes an item, while fields remain separately private. Use `pub(crate)` or `pub(super)` for narrower visibility. Re-export supported names with `pub use` so users see a stable path independent of internal layout.

Module paths can begin with `crate`, `self`, or `super`, or with a name brought into scope by `use`. Prefer paths that make ownership clear. A `use` statement creates a shorter local name; it does not copy code or make a private item public.

Put reusable behavior in `src/lib.rs`. A binary in `src/main.rs` can call that library through the package's crate name, where hyphens become underscores in Rust code. Keeping command-line orchestration small makes library behavior easier to test.

Keep dependencies directed. If modules require each other's internals, extract a lower-level responsibility or pass a trait later. Avoid broad public modules that expose implementation details.

Start with one package and split crates only when a boundary has a real purpose, such as reuse, separate deployment, or dependency isolation. Extra crates create extra public contracts and build configuration.

## Check your understanding

You are ready when you can distinguish package, crate, module, path, and visibility.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
