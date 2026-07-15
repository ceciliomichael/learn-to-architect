# Exercise Solutions: Slices, str, and String

```rust
fn word_count(text: &str) -> usize {
    text.split_whitespace().count()
}

fn first_word(text: &str) -> &str {
    text.split_whitespace().next().unwrap_or("")
}

fn sum(values: &[i32]) -> i32 {
    values.iter().sum()
}

fn double(values: &mut [i32]) {
    for value in values {
        *value *= 2;
    }
}

fn main() {
    let text = "Go\u{4e16}\u{754c}";
    println!("bytes: {:?}", text.bytes().collect::<Vec<_>>());
    println!("chars: {:?}", text.chars().collect::<Vec<_>>());
    println!(
        "{} {}",
        word_count("clear Rust course"),
        first_word("clear Rust")
    );

    let mut values = vec![1, 2, 3];
    println!("{}", sum(&values));
    double(&mut values);
    println!("{values:?}");
}
```
