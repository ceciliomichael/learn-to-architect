# Exercises: Module 33

Work locally and explain your choices.

## 1. Trace

Why is a Rust slice normally represented as pointer plus length at a C ABI instead of passing &[T] directly as a universal C type?

## 2. Repair

Change a safe extern function that dereferences an arbitrary pointer into an unsafe function with a documented Safety contract, then expose a safe Rust wrapper for slice callers.

## 3. Modify

Add a second safe wrapper accepting Option<&[i32]> and define clearly how None maps to the FFI representation without creating an invalid nonzero-length null pointer combination.

## 4. Build

Design a C-facing API for processing a byte buffer and returning an error code. Specify pointer validity, length, output buffer ownership, error values, thread-safety assumptions, and panic policy before writing implementation code.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
