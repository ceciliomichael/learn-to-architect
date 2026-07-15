# Exercise Solutions: Borrow with References

```rust
fn text_length(text: &String) -> usize {
    text.len()
}

fn append_course(text: &mut String) {
    text.push_str(" course");
}

fn main() {
    let mut title = String::from("Rust");
    let first = &title;
    let second = &title;
    println!("{} {} {}", first, second, text_length(&title));

    append_course(&mut title);
    println!("{title}");
}
```

The mutable borrow begins after the last use of both shared references. A local String is dropped when its function returns, so a returned reference to it would point to invalid data.
