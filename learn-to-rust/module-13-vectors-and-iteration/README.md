# Module 13: Vectors and Iteration

## What you will learn

You will store growable ordered values and borrow them without invalidating references.

```rust
fn main() {
    let mut tasks = vec![String::from("read")];
    tasks.push(String::from("practice"));
    for task in &tasks {
        println!("{task}");
    }
}
```

`Vec<T>` owns contiguous elements of one type. `push` may reallocate, so Rust rejects holding an element reference across a possible growth operation. Use `.get(index)` for Option-based lookup; indexing panics when out of bounds.

Use indexing only when an invalid index would mean the program itself is wrong. Use `get` when absence is possible and should be handled. `first`, `last`, `pop`, and slice methods often express intent more clearly than a numeric index.

Iterating `&values` borrows, `&mut values` mutably borrows, and `values` consumes. `retain` filters in place; building a new vector can make ownership clearer. Capacity is reserved storage, not initialized length.

`len` reports initialized elements. `capacity` reports how many elements fit before another allocation may be needed. Reserve capacity when a measured or naturally known size makes it useful, not as a default guess. Removing from the middle shifts later elements, while `swap_remove` is faster when order does not matter.

Keep references short. Read a value, finish using the reference, and only then grow or reorganize the vector. This order makes both the ownership rule and the intended work easy to see.

## Check your understanding

You are ready when you can choose consuming, shared, or mutable iteration.
