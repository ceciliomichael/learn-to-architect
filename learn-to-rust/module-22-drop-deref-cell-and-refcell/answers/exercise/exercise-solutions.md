# Exercise solution

```rust
use std::cell::Cell;

struct CallCounter {
    calls: Cell<u32>,
}

impl CallCounter {
    fn new() -> Self {
        Self {
            calls: Cell::new(0),
        }
    }

    fn record(&self) {
        self.calls.set(self.calls.get() + 1);
    }

    fn count(&self) -> u32 {
        self.calls.get()
    }
}

fn main() {
    let counter = CallCounter::new();
    counter.record();
    counter.record();
    counter.record();
    println!("{}", counter.count());
}
```

`u32` implements `Copy`, so `Cell` can move copied values in and out without exposing a reference to its contents.
