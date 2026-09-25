# Module 29: Drop, Deref, Cell, and RefCell

## Outcome

Understand RAII cleanup, pointer-like dereferencing, and interior mutability with Cell and RefCell without treating runtime borrow checking as a shortcut around design.

## Why this matters

Rust sometimes needs mutation behind a shared outer reference, especially in single-threaded implementation details such as counters, caches, or test doubles. It also lets types customize cleanup and pointer-like access behavior.

## Programming concept

RAII ties resource cleanup to object lifetime. Dereferencing accesses a value through an indirection layer. Interior mutability moves some mutation checks from ordinary compile-time borrowing rules into a controlled abstraction, sometimes enforced at runtime.

## Rust model

Drop runs when an owned value is destroyed. Deref lets smart-pointer-like types expose a target reference. Cell<T> supports copy/set-style interior mutation for suitable values without handing out references to the interior. RefCell<T> enforces shared-versus-exclusive borrow rules at runtime and panics when those rules are violated.

## Local Cargo example

Create cargo new interior_mutability --edition 2024 and replace src/main.rs.

~~~rust
use std::cell::{Cell, RefCell};

struct Metrics {
    requests: Cell<u64>,
    labels: RefCell<Vec<String>>,
}

impl Metrics {
    fn record(&self, label: &str) {
        self.requests.set(self.requests.get() + 1);
        self.labels.borrow_mut().push(label.to_owned());
    }
}

fn main() {
    let metrics = Metrics {
        requests: Cell::new(0),
        labels: RefCell::new(Vec::new()),
    };

    metrics.record("start");
    metrics.record("finish");

    println!("requests: {}", metrics.requests.get());
    println!("labels: {:?}", metrics.labels.borrow());
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- record receives &self even though implementation details mutate.
- Cell exposes get/set operations rather than references into its value.
- RefCell hands out Ref or RefMut guards and checks borrowing rules dynamically.
- This is single-threaded interior mutability; thread synchronization is taught later.
- The public API should still preserve clear invariants despite internal mutation.

## Deliberate mistake

~~~rust
use std::cell::RefCell;

fn main() {
    let values = RefCell::new(vec![1, 2]);
    let first = values.borrow_mut();
    let second = values.borrow_mut();
    println!("{} {}", first.len(), second.len());
}
~~~

RefCell cannot reject the conflict at compile time, so the second overlapping mutable borrow panics at runtime.

Corrected direction:

~~~rust
use std::cell::RefCell;

fn main() {
    let values = RefCell::new(vec![1, 2]);

    {
        let mut first = values.borrow_mut();
        first.push(3);
    }

    let second = values.borrow();
    println!("{second:?}");
}
~~~

## Mental model

- Drop expresses deterministic cleanup owned by a type.
- Deref should make pointer-like access natural, not create surprising domain conversions.
- Cell and RefCell allow interior mutation; they do not remove borrow rules.
- RefCell moves enforcement to runtime and therefore introduces possible borrow panic.
- Prefer ordinary ownership and &mut when they model the problem directly.

## Common mistakes

- Implementing Deref for ordinary domain conversion.
- Using RefCell to avoid understanding an ownership design.
- Holding RefMut guards across more code than necessary.
- Assuming RefCell is thread-safe.
- Calling drop methods directly instead of using std::mem::drop when early destruction is required.

## Transfer to other languages

RAII, destructors, reference proxies, interior mutability, and runtime borrow guards have analogues across systems and managed languages. The general concern is who can mutate shared state and when cleanup occurs.

## Guided practice

1. Create a type with Drop that prints a non-sensitive cleanup message in a disposable program.
2. Use std::mem::drop to end one owned value early.
3. Use Cell as a simple counter behind &self.
4. Trigger and then repair a RefCell borrow panic.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- explain RAII and Drop;
- state the purpose of Deref;
- choose Cell versus RefCell at a basic level;
- explain how RefCell can panic;
- prefer compile-time borrowing when practical.

## Next

Continue to [Module 30](../30-trait-objects-and-dynamic-dispatch/README.md).
