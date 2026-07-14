# Exercise solution

```rust
fn shorter<'a>(left: &'a str, right: &'a str) -> &'a str {
    if left.len() <= right.len() {
        left
    } else {
        right
    }
}

struct Snippet<'a> {
    text: &'a str,
}

impl Snippet<'_> {
    fn word_count(&self) -> usize {
        self.text.split_whitespace().count()
    }
}

fn main() {
    let first = String::from("a short note");
    let second = String::from("a much longer note for today");
    let snippet = Snippet {
        text: shorter(&first, &second),
    };

    println!("{}", snippet.text);
    println!("{} words", snippet.word_count());
}
```

The `Snippet` cannot remain usable after the selected source string is dropped. Rust verifies this relationship at compile time.
