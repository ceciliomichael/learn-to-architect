# Exercise solution

```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (sender, receiver) = mpsc::channel();
    let mut handles = Vec::new();

    for worker in 1..=3 {
        let worker_sender = sender.clone();
        handles.push(thread::spawn(move || worker_sender.send(worker)));
    }
    drop(sender);

    let mut messages: Vec<i32> = receiver.into_iter().collect();
    messages.sort();
    println!("{messages:?}");

    for handle in handles {
        match handle.join() {
            Ok(Ok(())) => {}
            Ok(Err(error)) => eprintln!("send failed: {error}"),
            Err(_) => eprintln!("worker panicked"),
        }
    }
}
```

Dropping the original sender is essential. Otherwise the receiver still sees a possible producer and waits for more messages.
