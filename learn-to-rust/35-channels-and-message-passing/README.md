# Module 35: Channels and Message Passing

## Outcome

Send owned messages between threads, design producer/consumer shutdown, use bounded queues for backpressure, and compare message passing with shared-state coordination.

## Why this matters

Threads often need to exchange work and results. Sharing every data structure behind locks couples workers tightly. Message passing can transfer ownership and make communication paths explicit.

## Programming concept

A channel is a queue connecting senders and receivers. Producers create messages and consumers process them. Backpressure prevents producers from generating work much faster than consumers can handle. Channel closure can be part of a clean shutdown protocol.

## Rust model

std::sync::mpsc provides multi-producer, single-consumer channels. channel is logically unbounded while sync_channel has bounded capacity and can block senders when full. Sender can be cloned for multiple producers. Receiving ends when all senders are dropped or disconnected.

## Local Cargo example

Create cargo new channels --edition 2024 and replace src/main.rs.

~~~rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (sender, receiver) = mpsc::sync_channel::<String>(2);

    let producer = thread::spawn(move || {
        for id in 1..=5 {
            sender.send(format!("job-{id}")).unwrap();
        }
    });

    for job in receiver {
        println!("processing {job}");
    }

    producer.join().unwrap();
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- sync_channel capacity 2 bounds queued messages.
- send may wait when the queue is full, applying backpressure to the producer.
- Sending a String transfers ownership of that message through the channel.
- The receiver for loop ends when all senders are dropped.
- The worker handle is joined so producer panic is not silently ignored.

## Deliberate mistake

~~~rust
use std::sync::mpsc;

fn main() {
    let (sender, receiver) = mpsc::channel();
    let retained = sender.clone();

    drop(sender);

    for message in receiver {
        println!("{message}");
    }

    drop(retained);
}
~~~

The receiver loop waits for disconnection, but retained is still a live sender and is dropped only after the loop that cannot finish. Shutdown is stuck.

Corrected direction:

~~~rust
use std::sync::mpsc;

fn main() {
    let (sender, receiver) = mpsc::channel();
    let retained = sender.clone();

    drop(sender);
    drop(retained);

    for message in receiver {
        println!("{message}");
    }
}
~~~

## Mental model

- Messages define communication contracts between concurrent components.
- Ownership transfer can avoid shared mutable data.
- Bound queues make overload visible through backpressure.
- Shutdown needs a protocol: explicit message, channel closure, cancellation, or a combination.
- Every sender clone can keep a receiver waiting for more messages.

## Common mistakes

- Using unbounded queues for unlimited external load without a memory strategy.
- Forgetting a sender clone during shutdown.
- Sending giant mutable domain objects when a smaller command/result message suffices.
- Calling send unwrap in production paths where receiver shutdown is ordinary.
- Assuming message order across independent producers is globally deterministic.

## Transfer to other languages

Actor systems, queues, mailboxes, event buses, job brokers, and channels all use message-passing concepts. Capacity, ordering, delivery guarantees, and failure modes differ, but flow control and shutdown remain core concerns.

## Guided practice

1. Send owned Strings and observe the sender can no longer use each moved message.
2. Clone a sender for two producers.
3. Use sync_channel with capacity 1 and slow the receiver to observe backpressure.
4. Handle SendError without panic.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- send owned messages between threads;
- explain bounded versus unbounded queues;
- design a channel shutdown path;
- identify when ownership transfer reduces shared-state complexity.

## Next

Continue to [Module 36](../36-shared-state-and-synchronization/README.md).
