# Module 14: Hash Maps and Hash Sets

## What you will learn

You will model key-value and unique-value collections with explicit ownership and no assumed order.

```rust
use std::collections::HashMap;

fn main() {
    let mut counts = HashMap::new();
    for word in "go rust go".split_whitespace() {
        *counts.entry(word).or_insert(0) += 1;
    }
    println!("{counts:?}");
}
```

Insertion moves owned keys and values unless they implement Copy. `get` returns a borrowed Option. The entry API handles insert-or-update without duplicate lookup.

Choose keys that have stable identity, such as an ID or normalized name. If two spellings should represent the same key, normalize and validate them before insertion. A map does not decide those domain rules for you. Use `contains_key` only when you need a yes-or-no answer; use `get` when you also need the value.

HashMap and HashSet iteration order is not stable. Sort copied keys for deterministic output. Keys require Eq and Hash contracts; do not mutate fields that determine hashing while stored.

HashSet provides union, intersection, difference, and membership for unique values.

Use a vector when order and duplicates matter, a hash set when uniqueness and membership matter, and a hash map when each key leads to a value. Selecting the collection from the problem is clearer than choosing one from habit.

## Check your understanding

You are ready when ownership, lookup, update, and output ordering are deliberate.
