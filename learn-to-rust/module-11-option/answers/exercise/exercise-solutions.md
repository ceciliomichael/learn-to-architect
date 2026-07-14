# Exercise Solutions: Optional Values with Option

```rust
fn find_name(id: u32) -> Option<String> {
    match id {
        1 => Some(String::from("Pen")),
        2 => Some(String::from("Book")),
        _ => None,
    }
}

fn main() {
    let name = find_name(2);
    match &name {
        Some(value) => println!("found {value}"),
        None => println!("not found"),
    }
    println!("borrowed: {:?}", name.as_deref());
    println!("length: {:?}", name.as_ref().map(String::len));
    let display = find_name(99).unwrap_or_else(|| String::from("Unknown"));
    println!("{display}");
}
```

The first match borrows `name`, so the later calls can still use it. `as_deref` exposes the string as borrowed `&str`. `map` runs only for `Some`, and `unwrap_or_else` creates the fallback only when the lookup returns `None`.
