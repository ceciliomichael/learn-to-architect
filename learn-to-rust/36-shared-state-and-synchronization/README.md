# Module 36: Shared State with Arc, Mutex, RwLock, and Atomics

## Outcome

Protect shared mutable state with synchronization, avoid common deadlock patterns, use RwLock and atomics only when their semantics fit, and compare shared state with message passing.

## Why this matters

Some state genuinely represents one shared resource: a cache, registry, coordination flag, or aggregate counter. Multiple threads need a strategy that prevents data races and defines when updates become visible.

## Programming concept

Mutual exclusion allows one critical section at a time. Read/write locks distinguish shared readers from exclusive writers. Atomics perform indivisible operations with explicit memory-ordering semantics. Deadlock occurs when threads wait on resources in a cycle that cannot make progress.

## Rust model

Mutex<T> guards T and returns a lock guard that releases the lock on Drop. Arc<Mutex<T>> combines shared ownership with synchronized mutation. RwLock<T> can allow multiple readers or one writer. Atomic types support lock-free individual operations; their Ordering argument defines synchronization semantics. Send and Sync constrain which types can cross or be shared between threads.

## Local Cargo example

Create cargo new shared_state --edition 2024 and replace src/main.rs.

~~~rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0_u64));
    let mut workers = Vec::new();

    for _ in 0..4 {
        let counter = Arc::clone(&counter);
        workers.push(thread::spawn(move || {
            for _ in 0..1_000 {
                let mut value = counter.lock().expect("counter mutex poisoned");
                *value += 1;
            }
        }));
    }

    for worker in workers {
        worker.join().expect("worker panicked");
    }

    println!("count: {}", *counter.lock().expect("counter mutex poisoned"));
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- Arc gives every worker ownership of the same Mutex allocation.
- Mutex gives one thread at a time mutable access to the counter.
- The guard unlocks automatically when it leaves scope.
- The example holds the lock for every increment; batching local increments would reduce contention.
- Poisoning reports that another thread panicked while holding the mutex; production code should choose a policy rather than calling expect blindly.

## Deliberate mistake

~~~rust
use std::sync::Mutex;

fn main() {
    let values = Mutex::new(vec![1, 2, 3]);
    let first = values.lock().unwrap();
    let second = values.lock().unwrap();
    println!("{} {}", first.len(), second.len());
}
~~~

A non-reentrant Mutex is already held by this thread when the second lock attempt occurs. Waiting for itself to release the first guard creates a self-deadlock.

Corrected direction:

~~~rust
use std::sync::Mutex;

fn main() {
    let values = Mutex::new(vec![1, 2, 3]);

    {
        let first = values.lock().unwrap();
        println!("{}", first.len());
    }

    let second = values.lock().unwrap();
    println!("{}", second.len());
}
~~~

## Mental model

- Keep lock scopes short and obvious.
- Do not perform slow network/file work while holding a lock unless the design explicitly requires it.
- Use a consistent global lock acquisition order when multiple locks must be held.
- RwLock helps only when read-heavy behavior and contention justify it.
- Atomics are not small mutex replacements; memory ordering must match the synchronization requirement.
- Prefer message passing when ownership transfer makes the interaction simpler.

## Common mistakes

- Wrapping all application state in one Arc<Mutex<_>>.
- Holding guards across unrelated work.
- Acquiring several locks in inconsistent orders.
- Using RwLock without measuring whether it improves contention.
- Using Ordering::Relaxed for coordination that actually requires ordering of other memory.
- Ignoring poisoning or worker panic policy.

## Transfer to other languages

Mutexes, reader-writer locks, atomics, deadlocks, contention, and memory ordering exist across concurrent languages. Rust prevents data races in safe code, but it cannot guarantee your lock protocol is deadlock-free or logically correct.

## Guided practice

1. Increment a shared counter through Arc<Mutex<_>>.
2. Refactor the worker to count locally and lock once to add a subtotal.
3. Create a read-heavy example using RwLock.
4. Use AtomicUsize with Ordering::Relaxed only for an independent statistics counter and explain why it is not synchronizing other data.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- explain Arc versus Mutex responsibilities;
- keep critical sections narrow;
- describe a deadlock cycle;
- state when RwLock may help;
- treat atomic ordering as a semantic design choice.

## Next

Continue to [Module 37](../37-async-futures-and-tokio/README.md).
