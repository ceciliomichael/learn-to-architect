# Exercise Solutions: Variables, Mutability, Constants, and Scalar Types

```rust
const MAX_ITEMS: usize = 100;

fn main() {
    let title = "Rust Foundations";
    let mut modules: u32 = 38;
    let price: f64 = 19.95;
    let available = true;
    let grade = 'A';
    modules += 1;

    let input = "  Rust  ";
    let input = input.trim();
    let input = input.len();

    println!("{title} {modules} {price:.2} {available} {grade}");
    println!("trimmed bytes: {input}, maximum: {MAX_ITEMS}");
}
```

Removing `mut` from `modules` makes the update fail. Restore it only for the binding that truly changes.
