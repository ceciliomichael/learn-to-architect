# Exercise solution

```rust
macro_rules! numbers {
    ($value:expr; $count:expr) => {
        vec![$value; $count]
    };
    ($($value:expr),* $(,)?) => {
        vec![$($value),*]
    };
}

fn main() {
    let listed = numbers![1, 2, 3];
    let repeated = numbers![5; 3];
    println!("{listed:?}");
    println!("{repeated:?}");
}
```

A function cannot accept both an arbitrary comma-separated expression list and the semicolon repetition syntax. The macro provides those two syntax forms and delegates their behavior to `vec!`.
