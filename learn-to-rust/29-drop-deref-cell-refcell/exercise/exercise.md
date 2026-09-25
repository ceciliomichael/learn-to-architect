# Exercises: Module 29

Work locally and explain your choices.

## 1. Trace

Why can a method taking &self update a Cell field without changing the method receiver to &mut self?

## 2. Repair

Create overlapping RefCell mutable borrows, observe the panic, then shorten the first guard before borrowing again.

## 3. Modify

Add a read-only labels snapshot method that clones the Vec intentionally and explain why an owned snapshot is desired.

## 4. Build

Create a single-threaded test spy that records method calls in RefCell<Vec<String>> through a trait method taking &self. Keep the interior mutability private.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
