# Module 01: Use the Rust Playground and Install Rust

## What you will learn

You will run Rust in a browser, recognize compiler feedback, and check a local stable toolchain.

Open <https://play.rust-lang.org/>, keep **Stable** selected, and run:

```rust
fn main() {
    println!("I am learning Rust.");
}
```

Use **Tools**, then **Rustfmt**, to apply standard formatting. The Playground is ideal for early single-file work, but it has no network and limits time, memory, and disk. Local Cargo is required later.

Install through <https://rustup.rs/>, then check:

```text
rustc --version
cargo --version
rustup show
```

Create a Rust 2024 project with `cargo new practice --edition 2024`, enter it, and run `cargo run`. Cargo manages packages, builds, tests, dependencies, and release profiles. `cargo check` type-checks quickly without producing a final executable.

Delete the semicolon after `println!` only after changing the line into invalid syntax, read the primary error and source pointer, then repair one cause. Compiler feedback is part of the learning process, not a failure of learning.

## Check your understanding

You are ready when you can run, format, break, repair, and rerun the first program online or locally.
