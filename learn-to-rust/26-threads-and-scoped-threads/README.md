# Module 26: Threads and Scoped Threads

An operating-system thread can run work at the same time as other threads. `thread::spawn` starts a thread and returns a `JoinHandle`. Always decide who joins it and how a panic is reported.

```rust
use std::thread;

fn main() {
    let values = vec![2, 4, 6];
    let handle = thread::spawn(move || values.iter().sum::<i32>());

    match handle.join() {
        Ok(total) => println!("{total}"),
        Err(_) => eprintln!("worker panicked"),
    }
}
```

`move` transfers the vector into the spawned closure because an ordinary spawned thread may outlive the calling scope. A scoped thread cannot outlive its `thread::scope` call, so it may safely borrow local data. The scope waits for its threads before returning.

Divide work only when the added coordination is worth it. Too many threads can increase memory use, scheduling overhead, and contention. Give each thread a clear input, output, and completion owner. Do not silently discard a join handle.

Thread panics do not automatically become normal application errors. `join` returns an error containing the panic payload. Convert it into an intentional report or recovery policy at the boundary.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 27](../27-channels-arc-mutex-and-shared-state/README.md).
