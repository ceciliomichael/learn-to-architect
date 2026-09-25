# Exercise Solutions: Module 37

Attempt the exercises before reading.

## 1. Trace

No. An async function call creates a future. The future must be driven by an executor through await, spawn, or another polling mechanism.

## 2. Repair

Use an async-aware timer for waiting. For genuinely blocking APIs, isolate them with spawn_blocking or another bounded blocking strategy rather than pretending they are async.

## 3. Modify

Create both futures and pass them to tokio::join!. The macro drives them concurrently on the runtime and returns both outputs.

## 4. Build

Use a semaphore or another explicit concurrency bound before starting each unit of work. Retain task handles or use a task set, apply timeout inside each unit, and collect a result enum so every requested job has a final state.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
