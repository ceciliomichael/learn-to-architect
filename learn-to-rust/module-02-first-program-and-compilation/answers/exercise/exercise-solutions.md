# Exercise Solutions: Compile and Run Your First Program

```rust
fn main() {
    // The report requires the learner and course on separate lines.
    println!("Learner: Ava");
    println!("Course: Rust Foundations");
    println!("{} modules, {} language, {} goal", 38, "Rust", "clarity");
}
```

Run `cargo run`, then `cargo build --release`. Debug artifacts are under `target/debug`; optimized artifacts are under `target/release`.
