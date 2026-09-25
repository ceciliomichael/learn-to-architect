# Exercises: Module 34

Work locally and explain your choices.

## 1. Trace

Why can thread::scope allow a worker to borrow local data that ordinary thread::spawn cannot borrow in the same way?

## 2. Repair

Spawn a closure that borrows a local String and repair it either by moving ownership or by using an appropriate scoped thread.

## 3. Modify

Split a vector into four borrowed chunks inside thread::scope and sum them, then combine joined results.

## 4. Build

Build a parallel word-count experiment that splits a fixed in-memory set of independent text chunks among scoped threads and returns per-thread counts. Compare against a single-threaded version for correctness before discussing speed.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
