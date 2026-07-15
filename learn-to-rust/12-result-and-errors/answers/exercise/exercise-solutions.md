# Exercise Solutions: Recoverable Errors with Result

```rust
use std::num::ParseIntError;

#[derive(Debug)]
enum QuantityError {
    Empty,
    Invalid(ParseIntError),
    Zero,
}

impl QuantityError {
    fn message(&self) -> String {
        match self {
            Self::Empty => String::from("quantity is required"),
            Self::Invalid(error) => format!("quantity must be a whole number: {error}"),
            Self::Zero => String::from("quantity must be positive"),
        }
    }
}

fn parse_quantity(text: &str) -> Result<u32, QuantityError> {
    let trimmed = text.trim();
    if trimmed.is_empty() {
        return Err(QuantityError::Empty);
    }
    let value = trimmed.parse().map_err(QuantityError::Invalid)?;
    if value == 0 {
        return Err(QuantityError::Zero);
    }
    Ok(value)
}

fn main() {
    match parse_quantity("3") {
        Ok(value) => println!("{value}"),
        Err(error) => eprintln!("{}", error.message()),
    }
}
```

The enum keeps the original parsing error in its `Invalid` variant. The `message` method reports it without requiring traits or lifetime syntax that come later in the course.
