# Module 07: Borrow with References

## What you will learn

You will lend access without transferring ownership and enforce shared or exclusive access through references.

```rust
fn length(text: &String) -> usize {
    text.len()
}

fn append_mark(text: &mut String) {
    text.push('!');
}

fn main() {
    let mut message = String::from("Ready");
    println!("{}", length(&message));
    append_mark(&mut message);
    println!("{message}");
}
```

`&T` is a shared reference. Several shared borrows may coexist while no mutation occurs. `&mut T` is an exclusive mutable reference. Only one mutable borrow can be active for that value, and it cannot overlap active shared borrows.

Borrow scopes usually end at the last use, not necessarily the closing brace. Reborrowing lets a function temporarily use an existing mutable reference without taking it permanently.

References must never outlive the value they reference. The compiler rejects dangling references. A function returning a reference must connect it to an input lifetime, taught explicitly later.

Use borrowing when a function needs temporary access. Use ownership when it must store, consume, or independently control the value.

## Check your understanding

You are ready when you can identify every owner, shared borrow, exclusive borrow, mutation, and last use.
