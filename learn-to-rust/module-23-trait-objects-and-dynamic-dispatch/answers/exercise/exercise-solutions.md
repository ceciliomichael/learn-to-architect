# Exercise solution

```rust
trait Notice {
    fn format(&self) -> String;
}

struct EmailNotice {
    address: String,
    subject: String,
}

struct ConsoleNotice {
    level: String,
    message: String,
}

impl Notice for EmailNotice {
    fn format(&self) -> String {
        format!("Email to {}: {}", self.address, self.subject)
    }
}

impl Notice for ConsoleNotice {
    fn format(&self) -> String {
        format!("{}: {}", self.level, self.message)
    }
}

fn main() {
    let notices: Vec<Box<dyn Notice>> = vec![
        Box::new(EmailNotice {
            address: String::from("learner@example.com"),
            subject: String::from("Lesson ready"),
        }),
        Box::new(ConsoleNotice {
            level: String::from("INFO"),
            message: String::from("Course opened"),
        }),
    ];

    for notice in notices {
        println!("{}", notice.format());
    }
}
```

The vector has one element type, `Box<dyn Notice>`, while the boxed values have different concrete types.
