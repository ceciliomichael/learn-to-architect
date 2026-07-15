# Module 27: Channels, Arc, Mutex, and Shared State

Channels transfer messages between threads. `mpsc::channel` has a sender and receiver. Cloned senders support multiple producers. Receiving ends after every sender is dropped, so retaining an unused sender can make a receiver wait forever.

Shared mutable state uses another pattern. `Arc<T>` provides shared ownership and `Mutex<T>` allows one thread at a time to access the inner value.

```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let total = Arc::new(Mutex::new(0));
    let worker_total = Arc::clone(&total);
    let handle = thread::spawn(move || {
        let mut guard = worker_total
            .lock()
            .unwrap_or_else(|error| error.into_inner());
        *guard += 1;
    });
    if handle.join().is_err() {
        eprintln!("worker panicked");
    }
}
```

A mutex becomes poisoned when a thread panics while holding it. Recovery is domain-specific: the value may still be valid, may need repair, or may require shutdown. Do not blindly ignore poisoning in important state.

Keep lock scopes short and never hold a lock while performing slow I/O. Acquire several locks in one consistent order to reduce deadlock risk. Atomic types can handle small independent counters and flags, but their ordering rules require separate study.

Prefer message passing when one owner can manage the data. Prefer a lock when several threads truly need synchronized access to the same value.

Continue to [Module 28](../28-async-futures-and-tokio/README.md).
