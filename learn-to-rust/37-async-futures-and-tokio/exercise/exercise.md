# Exercises: Module 37

Work locally and explain your choices.

## 1. Trace

If you call an async fn and store the returned future but never await, spawn, or otherwise poll it, should you assume the operation completed?

## 2. Repair

Place std::thread::sleep inside an async function, explain why it can stall runtime progress, and replace it with tokio::time::sleep.

## 3. Modify

Run two simulated_lookup calls concurrently with tokio::join! and print both values.

## 4. Build

Build a bounded async job runner. Accept a fixed Vec of job IDs, process at most three simultaneously, apply a per-job timeout, collect success/timeout results, and finish only after all launched work is accounted for.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
