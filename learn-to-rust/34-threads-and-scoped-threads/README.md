# Module 34: Threads and Scoped Threads

## Outcome

Create and join OS threads, move owned work into threads, borrow safely with scoped threads, and distinguish concurrency from parallelism.

## Why this matters

Some programs need work to progress independently or use multiple CPU cores. Concurrency introduces scheduling and shared-resource problems that do not exist in single-threaded code.

## Programming concept

A process can contain multiple threads that share process resources while having independent execution stacks. Concurrency means tasks can make progress during overlapping time; parallelism means tasks actually execute simultaneously. Scheduling order is generally not deterministic.

## Rust model

std::thread::spawn creates an owned thread whose closure normally needs data valid for the thread's possible lifetime, often using move. JoinHandle::join waits for completion and reports thread panic. thread::scope allows threads to borrow data whose lifetime is bounded by the scope. Send and Sync traits describe whether types may be transferred or shared across threads safely.

## Local Cargo example

Create cargo new threads --edition 2024 and replace src/main.rs.

~~~rust
use std::thread;

fn main() {
    let values = vec![10, 20, 30, 40];

    thread::scope(|scope| {
        let first_half = &values[..2];
        let second_half = &values[2..];

        let left = scope.spawn(|| first_half.iter().sum::<i32>());
        let right = scope.spawn(|| second_half.iter().sum::<i32>());

        println!("sum: {}", left.join().unwrap() + right.join().unwrap());
    });

    println!("values still owned here: {values:?}");
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- thread::scope guarantees its child threads finish before the scope exits.
- That guarantee allows child threads to borrow slices from values safely.
- Each worker computes independently and returns a value through its JoinHandle.
- join waits for completion and also surfaces a thread panic as an error value.
- After the scope ends, main still owns the vector.

## Deliberate mistake

~~~rust
use std::thread;

fn main() {
    let message = String::from("hello");

    let worker = thread::spawn(|| {
        println!("{message}");
    });

    worker.join().unwrap();
}
~~~

A spawned thread may outlive the current stack frame, so an ordinary borrowed capture of a local String is not accepted for thread::spawn.

Corrected direction:

~~~rust
use std::thread;

fn main() {
    let message = String::from("hello");

    let worker = thread::spawn(move || {
        println!("{message}");
    });

    worker.join().unwrap();
}
~~~

## Mental model

- A thread introduces independent scheduling.
- Join threads whose completion or result matters.
- Use move when ownership should transfer into an unscoped worker.
- Use scoped threads when bounded child work can borrow parent data safely.
- Send and Sync are type-level thread-safety capabilities, not performance guarantees.
- More threads can make a program slower when work is small, contended, or I/O strategy is wrong.

## Common mistakes

- Assuming thread execution order.
- Spawning threads and dropping handles when completion matters.
- Using threads for tiny work without measuring overhead.
- Sharing mutation before choosing a synchronization strategy.
- Treating concurrency and parallelism as identical.

## Transfer to other languages

Threads, tasks, worker pools, and schedulers exist across platforms. Rust's type system rejects many invalid sharing patterns earlier, but nondeterministic scheduling, contention, and work partitioning remain universal concerns.

## Guided practice

1. Spawn one owned worker and join it.
2. Return a numeric result through JoinHandle.
3. Use thread::scope to borrow two disjoint slices.
4. Run a multi-threaded printing example several times and observe that scheduling order is not a contract.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- distinguish concurrency and parallelism;
- spawn and join a thread;
- explain move capture for thread::spawn;
- use scoped threads for borrowed work;
- describe Send and Sync at a conceptual level.

## Next

Continue to [Module 35](../35-channels-and-message-passing/README.md).
