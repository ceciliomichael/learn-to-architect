# Module 16: Hash Maps and Hash Sets

## Outcome

Model key-value lookup and uniqueness with HashMap and HashSet, update entries safely, and choose collections based on access needs.

## Why this matters

Scanning a vector for every lookup is often the wrong model when data has stable keys such as IDs or names. Other problems care only whether a value appears uniquely.

## Programming concept

A map associates unique keys with values. A set stores unique keys without separate values. Hash-based structures use a hash of the key to organize lookup. Ordering is not their primary contract.

## Rust model

std::collections::HashMap<K,V> stores associations and HashSet<T> stores unique values. get borrows by key, insert adds or replaces, and entry supports conditional insertion or update. Owned keys and values moved into a collection become owned by it.

## Local Cargo example

Create a project named maps_sets and import std::collections::{HashMap, HashSet}.

~~~rust
use std::collections::{HashMap, HashSet};

fn main() {
    let mut counts = HashMap::new();

    for word in ["rust", "safe", "rust", "fast"] {
        *counts.entry(word).or_insert(0) += 1;
    }

    println!("rust count: {:?}", counts.get("rust"));

    let unique: HashSet<_> = ["red", "blue", "red"].into_iter().collect();
    println!("unique colors: {}", unique.len());
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- entry gives access to a key whether it is present or absent.
- or_insert supplies a default and returns a mutable reference to the stored value.
- HashSet collection removes duplicate logical keys.
- Borrowed lookup does not require creating a new owned key in common cases.
- Do not rely on hash iteration order for user-facing ordering.

## Deliberate mistake

~~~rust
use std::collections::HashMap;

fn main() {
    let mut users = HashMap::new();
    let key = String::from("ada");
    let value = String::from("active");
    users.insert(key, value);
    println!("{key}: {value}");
}
~~~

The owned key and value moved into the map. The map owns them after insertion.

Corrected direction:

~~~rust
use std::collections::HashMap;

fn main() {
    let mut users = HashMap::new();
    users.insert(String::from("ada"), String::from("active"));

    if let Some(status) = users.get("ada") {
        println!("ada: {status}");
    }
}
~~~

## Mental model

- Choose collections from required operations and invariants.
- Maps model association, sets uniqueness, vectors ordered sequences.
- Insertion of owned values normally transfers ownership.
- Use entry when behavior depends on presence or absence.
- Hash iteration order is not a stable presentation contract.

## Common mistakes

- Expecting sorted HashMap output.
- Cloning keys automatically instead of designing ownership.
- Using a map when duplicate ordered records matter.
- Using a set when associated values are required.
- Doing repeated lookup work that entry can express once.

## Transfer to other languages

Dictionaries, maps, hash tables, and sets appear in many languages. Equality, hashing, ordering, and ownership vary, but data-structure selection from required operations is universal.

## Guided practice

1. Count repeated words with entry.
2. Check membership in a HashSet.
3. Insert the same key twice and observe replacement.
4. Move owned strings into a map and look them up by borrowed text.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- choose among Vec, HashMap, and HashSet;
- update counts with entry;
- predict ownership after insertion;
- avoid relying on hash order.

## Next

Continue to [Module 17](../17-modules-crates-packages-and-visibility/README.md).
