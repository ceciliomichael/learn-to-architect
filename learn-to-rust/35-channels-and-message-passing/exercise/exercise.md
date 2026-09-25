# Exercises: Module 35

Work locally and explain your choices.

## 1. Trace

Why can one forgotten Sender clone keep a receiver iteration waiting?

## 2. Repair

Create a shutdown deadlock by retaining a sender until after receiver iteration, then drop all senders before waiting for disconnect.

## 3. Modify

Use two producers with cloned senders and include producer ID in each message.

## 4. Build

Build a bounded worker-input queue with one producer and one consumer. Define a Job enum with Work(String) and Shutdown variants, and compare explicit Shutdown with drop-based closure.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
