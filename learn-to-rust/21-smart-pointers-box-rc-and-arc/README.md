# Module 21: Smart Pointers with Box, Rc, and Arc

Smart pointers own or manage values while also acting like references.

`Box<T>` gives one owner to a value stored on the heap. It is useful when a type's size would otherwise be recursive.

```rust
enum List {
    Node(i32, Box<List>),
    End,
}
```

`Rc<T>` provides shared ownership inside one thread. Cloning an `Rc` increases a reference count; it does not clone the inner value. The value is dropped after the last owner is dropped.

`Arc<T>` is the thread-safe form of reference-counted ownership. It makes ownership sharing safe across threads, but it does not automatically make inner mutation safe. Module 27 combines it with synchronization.

Reference counting can leak memory when strong references form a cycle. Use `Weak<T>` for non-owning links such as a child pointing back to its parent. A weak reference must be upgraded because the value may already be gone.

Choose the smallest ownership tool that fits:

- Ordinary ownership for one known owner.
- A reference for temporary access.
- `Box` for one owner with heap placement or recursive size.
- `Rc` for several owners in one thread.
- `Arc` for several owners across threads.

Smart pointers solve ownership structure. They should not replace a simpler data model that avoids shared ownership.

Continue to [Module 22](../22-drop-deref-cell-and-refcell/README.md).
