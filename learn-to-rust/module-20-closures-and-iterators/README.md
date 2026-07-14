# Module 20: Closures and Iterators

A closure is an unnamed function that can use values from its surrounding scope.

```rust
fn main() {
    let minimum = 10;
    let accepted = [4, 10, 18, 7]
        .iter()
        .filter(|number| **number >= minimum)
        .count();
    println!("{accepted}");
}
```

Closures capture values by shared borrow, mutable borrow, or ownership according to how they use them. `move` asks a closure to take ownership of captured values, which is useful when work may outlive the current scope.

The closure traits describe capture behavior:

- `Fn` can be called through a shared reference.
- `FnMut` may change captured state.
- `FnOnce` may consume captured values and can always be called at least once.

An iterator produces one item at a time. Adaptors such as `map`, `filter`, and `take` are lazy. Nothing is processed until a consumer such as `collect`, `sum`, `count`, or a `for` loop asks for items.

Choose ownership deliberately: `iter()` borrows items, `iter_mut()` mutably borrows them, and `into_iter()` consumes the collection. Iterator chains can be concise, but a loop is better when the chain becomes difficult to explain or needs complex error handling.

Continue to [Module 21](../module-21-smart-pointers-box-rc-and-arc/README.md).
