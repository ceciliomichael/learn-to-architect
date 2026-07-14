# Exercise Solutions: Hash Maps and Hash Sets

```rust
use std::collections::{HashMap, HashSet};

fn main() {
    let mut counts = HashMap::new();
    for word in "rust is clear and rust is safe".split_whitespace() {
        *counts.entry(word.to_owned()).or_insert(0) += 1;
    }
    println!("missing: {:?}", counts.get("missing"));
    let mut keys: Vec<_> = counts.keys().collect();
    keys.sort();
    for key in keys {
        println!("{key} {}", counts[key]);
    }

    let required: HashSet<_> = ["ownership", "borrowing", "errors"].into_iter().collect();
    let completed: HashSet<_> = ["ownership", "errors"].into_iter().collect();
    println!(
        "missing: {:?}",
        required.difference(&completed).collect::<Vec<_>>()
    );
    println!(
        "shared: {:?}",
        required.intersection(&completed).collect::<Vec<_>>()
    );
}
```

`entry(...).or_insert(0)` returns mutable access to the count, so one lookup handles both a new word and an existing word. Keys are sorted before display because hash-map order is not a promise. The set difference finds required topics not completed, while the intersection finds topics in both sets.
