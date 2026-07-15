# Exercise Solutions: Modules, Crates, Packages, and Visibility

`src/lib.rs`:

```rust
mod price {
    fn valid(cents: i64, quantity: i64) -> bool {
        cents >= 0 && quantity >= 0
    }
    pub fn subtotal(cents: i64, quantity: i64) -> Option<i64> {
        valid(cents, quantity).then_some(cents * quantity)
    }
}

pub use price::subtotal;
```

`src/main.rs`:

```rust
fn main() {
    println!("{:?}", rust_practice::subtotal(125, 3));
}
```

Use package name `rust-practice`, which imports as `rust_practice`. Run `cargo fmt`, `cargo check`, `cargo test`, and `cargo doc --no-deps`.

The private `valid` helper remains an implementation detail. Re-exporting `subtotal` gives callers the short stable path `rust_practice::subtotal`, even though the function is organized inside the private `price` module.
