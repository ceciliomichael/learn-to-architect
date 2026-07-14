# Exercise Solutions: Ownership, Moves, Copy, and Clone

```rust
fn return_text(text: String) -> String {
    println!("received: {text}");
    text
}

fn main() {
    let first = String::from("moved");
    let second = first;
    println!("{second}");

    let count = 4;
    let copied = count;
    println!("{count} {copied}");

    let original = String::from("cloned");
    let independent = original.clone();
    println!("{original} {independent}");

    let returned = return_text(String::from("round trip"));
    println!("{returned}");
}
```

Repair a use-after-move by using the new owner, borrowing in the next module, returning ownership, or cloning only when independent ownership is actually required.
