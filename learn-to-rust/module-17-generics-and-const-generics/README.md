# Module 17: Generics and Const Generics

Generics let one piece of code work with several types while keeping Rust's type checks. A name such as `T` stands for a type chosen by the caller.

```rust
fn first<T>(items: &[T]) -> Option<&T> {
    items.first()
}

fn main() {
    println!("{:?}", first(&[10, 20, 30]));
    println!("{:?}", first(&["red", "blue"]));
}
```

The function does not need to know how to print, compare, or copy `T`. It only asks the slice for a reference. When code needs an ability such as comparison, a trait bound will state that requirement in Module 18.

Generic structs and enums work the same way:

```rust
struct Pair<T> {
    left: T,
    right: T,
}
```

A const generic is a value known at compile time. Array length is a common example.

```rust
fn last<T, const N: usize>(items: &[T; N]) -> Option<&T> {
    items.last()
}
```

Rust creates suitable machine code for the concrete types used by the program. This is called monomorphization. Generics do not mean every function should be abstract. Use a concrete type when only one type makes sense or when it makes the contract clearer.

## What you should remember

- Type parameters remove repeated code without removing type safety.
- A generic function may only use abilities stated in its bounds.
- Const parameters represent compile-time values such as array lengths.
- Prefer meaningful names such as `Item` when several type parameters are present.

Continue to [Module 18](../module-18-traits-and-trait-bounds/README.md).
