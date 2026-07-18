# Module 35: Threads, Processes, and Queues

## What you will learn

You will choose a concurrency model from the workload, protect shared state, and shut workers down predictably.

## Concurrency is overlapping progress

Concurrency does not automatically make work faster. It adds scheduling, coordination, failure, and cleanup costs.

- I/O-bound work spends time waiting for files, networks, or databases.
- CPU-bound work spends time calculating.

In standard CPython 3.12, the global interpreter lock means only one thread executes Python bytecode at a time in one process, although I/O and some extension work release it. Threads can still help overlapping I/O. Separate processes can run Python CPU work in parallel on multiple cores.

Later Python releases offer optional free-threaded builds, but code must still synchronize shared mutable state. Do not write a baseline course as though the GIL were a safety lock for application invariants.

## Use futures for task results

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

def read_size(path):
    return path, path.stat().st_size

with ThreadPoolExecutor(max_workers=4) as executor:
    futures = [executor.submit(read_size, path) for path in paths]
    for future in as_completed(futures):
        path, size = future.result()
        print(path, size)
```

`future.result()` returns the value or reraises the worker exception. Always observe results. The executor context waits for shutdown.

## Protect compound shared updates

```python
from threading import Lock

lock = Lock()
total = 0

def add(value):
    global total
    with lock:
        total += value
```

A read-modify-write sequence is not a domain-level atomic guarantee. Prefer avoiding shared mutation by returning results to one owner. When locking is required, hold locks briefly and acquire multiple locks in a consistent order.

## Use queues for ownership transfer

`queue.Queue` coordinates threads safely. Producers put messages and consumers get them. Define sentinel or shutdown behavior, call `task_done` for completed tasks when using `join`, and make sure failures do not leave unfinished counts forever.

## Processes isolate memory

```python
from concurrent.futures import ProcessPoolExecutor

def square(value: int) -> int:
    return value * value

def main() -> None:
    with ProcessPoolExecutor() as executor:
        print(list(executor.map(square, range(10))))

if __name__ == "__main__":
    main()
```

The main guard is essential for safe process startup on spawn-based platforms such as Windows. Submitted callables and arguments must be serializable for process transfer. Process startup and copying can exceed benefits for small tasks.

## Cancellation and shutdown are cooperative

Cancelling a future usually cannot stop work already running. Define timeouts, stop accepting new tasks, signal cooperative shutdown, drain or abandon queues by policy, wait for workers, and close resources.

## Check your understanding

You are ready when you can choose threads for waiting, processes for substantial CPU work, and avoid shared state where result collection is simpler.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
