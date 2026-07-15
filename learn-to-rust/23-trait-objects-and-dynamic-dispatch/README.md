# Module 23: Trait Objects and Dynamic Dispatch

Generics choose concrete implementations at compile time. A trait object, written `dyn Trait`, allows one value to hold any type that implements a suitable trait.

```rust
trait Draw {
    fn draw(&self) -> String;
}

struct Button;

impl Draw for Button {
    fn draw(&self) -> String {
        String::from("[button]")
    }
}

fn render(items: &[Box<dyn Draw>]) {
    for item in items {
        println!("{}", item.draw());
    }
}
```

This is dynamic dispatch: Rust selects the implementation while the program runs. It permits heterogeneous collections and stable boundaries where callers should not depend on concrete types. It also adds pointer indirection and prevents some compiler optimizations.

Not every trait can be used as a trait object. Its callable methods must be compatible with a value whose concrete type is hidden. Compiler messages will identify methods that violate these object-safety rules.

Use generics when one concrete type is known for each call and performance or static guarantees matter. Use trait objects when values of different types must share one collection or the concrete type must remain hidden. Avoid frequent downcasting because it works against the shared trait contract. If callers constantly ask for concrete types, an enum may describe the closed set more clearly.

Continue to [Module 24](../24-files-paths-and-streamed-io/README.md).
