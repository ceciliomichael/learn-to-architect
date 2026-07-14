# Exercise Solutions: Expressions, Conditions, Loops, and Match Basics

```rust
fn main() {
    let score = 82;
    let label = if score >= 90 {
        "excellent"
    } else if score >= 75 {
        "good"
    } else if score >= 60 {
        "passing"
    } else {
        "review"
    };

    let mut total = 0;
    for number in 1..=100 {
        total += number;
    }

    let mut count = 3;
    while count > 0 {
        count -= 1;
    }

    let result = loop {
        break 25;
    };

    let word = match 2 {
        1 => "one",
        2 => "two",
        3 => "three",
        _ => "other",
    };
    println!("{label} {total} {result} {word}");
}
```
