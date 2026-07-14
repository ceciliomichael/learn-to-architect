# Exercise solution

```rust
fn get_checked(values: &[i32], index: usize) -> Option<i32> {
    if index >= values.len() {
        return None;
    }

    // SAFETY: The check above proves index is smaller than values.len().
    Some(unsafe { *values.get_unchecked(index) })
}

fn main() {
    assert_eq!(get_checked(&[], 0), None);
    assert_eq!(get_checked(&[10, 20, 30], 0), Some(10));
    assert_eq!(get_checked(&[10, 20, 30], 2), Some(30));
    assert_eq!(get_checked(&[10, 20, 30], 3), None);
    println!("all checks passed");
}
```

Production code should use `values.get(index).copied()`. It already expresses this operation safely and clearly, with no manual invariant to maintain.
