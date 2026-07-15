# Module 22: Drop, Deref, Cell, and RefCell

Rust cleans up owned resources when their owners leave scope. This pattern is called RAII. A type can implement `Drop` to release a resource. Call `std::mem::drop(value)` when cleanup must happen early; Rust does not allow calling `value.drop()` directly.

The `Deref` trait lets smart pointers behave like references for many operations. Deref coercion is why a `&String` can often be passed where `&str` is expected. Custom `Deref` implementations should preserve pointer-like meaning, not hide unrelated conversions.

Interior mutability permits mutation through a shared reference while preserving rules in another way:

- `Cell<T>` copies values in and out and is suited to small `Copy` values.
- `RefCell<T>` checks the one-writer-or-many-readers rule while the program runs.

```rust
use std::cell::RefCell;

fn main() {
    let messages = RefCell::new(Vec::new());
    messages.borrow_mut().push("started");
    println!("{:?}", messages.borrow());
}
```

Breaking a `RefCell` borrowing rule causes a panic, not a compile error. Keep `borrow()` and `borrow_mut()` guards in small scopes. `Cell` and `RefCell` are for single-threaded code. Cross-thread shared state needs the tools in Module 27.

Interior mutability is valuable for focused state hidden behind a clear contract. If it spreads through the design, reconsider who should own the mutable value.

Continue to [Module 23](../23-trait-objects-and-dynamic-dispatch/README.md).
