# Exercise solution

```rust
trait Describe {
    fn name(&self) -> &str;

    fn describe(&self) -> String {
        format!("Item: {}", self.name())
    }
}

struct Book {
    name: String,
}

struct Tool {
    name: String,
    category: String,
}

impl Describe for Book {
    fn name(&self) -> &str {
        &self.name
    }
}

impl Describe for Tool {
    fn name(&self) -> &str {
        &self.name
    }

    fn describe(&self) -> String {
        format!("Item: {} ({})", self.name, self.category)
    }
}

fn show<T: Describe>(item: &T) {
    println!("{}", item.describe());
}

fn main() {
    let book = Book {
        name: String::from("Rust Notes"),
    };
    let tool = Tool {
        name: String::from("Hammer"),
        category: String::from("Hand tool"),
    };
    show(&book);
    show(&tool);
}
```

`show` only depends on the small `Describe` contract, not on either concrete struct.
