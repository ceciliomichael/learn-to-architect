# Module 28: Smart Pointers with Box, Rc, and Arc

## Outcome

Explain indirection and shared ownership, choose Box, Rc, or Arc for specific ownership needs, and recognize reference-count cycles.

## Why this matters

Ordinary ownership is enough for most Rust code, but some structures need indirection or more than one owner. Recursive data needs a known-size indirection point, and shared read-mostly data may have several legitimate owners.

## Programming concept

Indirection stores or accesses a value through another object rather than embedding it directly. Reference counting tracks how many owners remain and cleans up after the final owner disappears. Shared ownership is different from shared mutability.

## Rust model

Box<T> owns one T through heap allocation and provides indirection. Rc<T> provides reference-counted shared ownership for single-threaded use. Arc<T> uses atomic reference counting so ownership can be shared across threads when T also satisfies the required thread-safety rules. Rc and Arc cloning increments an ownership count; it does not deep-clone T.

## Local Cargo example

Create cargo new smart_pointers --edition 2024 and replace src/main.rs.

~~~rust
use std::rc::Rc;

enum List {
    Cons(i32, Box<List>),
    Nil,
}

fn main() {
    let list = List::Cons(1, Box::new(List::Cons(2, Box::new(List::Nil))));

    if let List::Cons(first, rest) = &list {
        println!("first: {first}");
        if let List::Cons(second, _) = rest.as_ref() {
            println!("second: {second}");
        }
    }

    let shared = Rc::new(String::from("shared configuration"));
    let owner_a = Rc::clone(&shared);
    let owner_b = Rc::clone(&shared);

    println!("owners: {}", Rc::strong_count(&shared));
    println!("{owner_a} / {owner_b}");
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- The recursive List needs Box because embedding List directly inside itself would have no finite compile-time size.
- Box still has one owner; it adds indirection rather than shared ownership.
- Rc wraps one String allocation with a single-threaded reference count.
- Rc::clone increments the reference count and is conventionally clearer than pretending a deep String clone occurred.
- The value is cleaned up after the last strong Rc owner is dropped.

## Deliberate mistake

~~~rust
use std::rc::Rc;
use std::thread;

fn main() {
    let value = Rc::new(String::from("hello"));
    thread::spawn(move || println!("{value}")).join().unwrap();
}
~~~

Rc does not implement the thread-safety capability required to transfer shared reference-count ownership between threads. Its count updates are not atomic.

Corrected direction:

~~~rust
use std::sync::Arc;
use std::thread;

fn main() {
    let value = Arc::new(String::from("hello"));
    let worker_value = Arc::clone(&value);

    thread::spawn(move || println!("{worker_value}"))
        .join()
        .unwrap();

    println!("{value}");
}
~~~

## Mental model

- Use Box for single ownership plus indirection.
- Use Rc only when multiple single-threaded owners are genuinely required.
- Use Arc for shared ownership that must cross threads.
- Cloning Rc or Arc clones the pointer owner, not the underlying T.
- Shared ownership does not automatically permit mutation.
- Reference-count cycles can keep values alive forever unless weak references or another design breaks the cycle.

## Common mistakes

- Using Rc or Arc when one clear owner would be simpler.
- Assuming Arc makes any inner type thread-safe.
- Calling Arc<Mutex<T>> the default shape for all shared state.
- Confusing Rc::clone with a deep clone of T.
- Building parent-child strong-reference cycles without considering Weak.

## Transfer to other languages

Indirection, reference counting, shared ownership, and weak references appear in C++, Swift, Python internals, .NET infrastructure, and many runtimes. Rust makes the ownership mode explicit in types.

## Guided practice

1. Place a large struct in Box and observe that ownership remains singular.
2. Clone an Rc several times and inspect strong_count.
3. Drop one Rc owner and inspect the count again.
4. Read about Weak and explain why it does not keep a value alive by itself.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- choose Box versus Rc versus Arc from ownership requirements;
- explain what reference-count clone means;
- state that shared ownership and mutation are separate concerns;
- identify a possible strong-reference cycle.

## Next

Continue to [Module 29](../29-drop-deref-cell-refcell/README.md).
