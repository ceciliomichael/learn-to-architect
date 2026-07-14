# Exercise Solutions: Use the Rust Playground and Install Rust

```rust
fn main() {
    println!("Rust checks my program.");
    println!("The compiler explains many mistakes.");
    println!("Then valid code runs.");
}
```

Local commands are:

```text
cargo new practice --edition 2024
cd practice
cargo check
cargo run
cargo fmt --check
```

Restore valid punctuation before the final checks. The local compiler version may be newer than the course baseline, but examples use stable Rust 1.90 and newer.
