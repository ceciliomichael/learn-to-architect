# Exercises: Module 30

Work locally and explain your choices.

## 1. Trace

Why can Vec<Box<dyn Formatter>> hold Upper and Prefix while Vec<Upper> cannot?

## 2. Repair

Create a trait-object-incompatible method shape, read the compiler explanation, and redesign the runtime contract around object-safe behavior.

## 3. Modify

Add a Lower formatter without changing the loop.

## 4. Build

Create a Reporter trait with console and in-memory implementations. Let one application function accept &dyn Reporter and emit domain messages without knowing the concrete reporter.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
