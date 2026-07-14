# Exercise solution

```rust
fn select_scores<F>(scores: &[i32], keep: F) -> Vec<i32>
where
    F: Fn(i32) -> bool,
{
    scores
        .iter()
        .copied()
        .filter(|score| keep(*score))
        .collect()
}

fn main() {
    let scores = vec![42, 81, 67, 95, 74];
    let selected = select_scores(&scores, |score| score >= 70);
    let total: i32 = selected.iter().sum();

    println!("selected: {selected:?}");
    println!("total: {total}");
    println!("original: {scores:?}");
}
```

The function borrows the slice. `copied` turns each borrowed `&i32` into an `i32`, which is inexpensive because integers implement `Copy`.
