# Exercise Solutions: Module 01

Use these after attempting the exercises.

## 1. Trace

`Cargo.toml` is project/package configuration and `src/main.rs` is source. `target/` is generated build output. Cargo may also create version-control metadata depending on the environment.

## 2. Repair

Restore the missing `)`. The lesson is to use the first parser diagnostic and its source location rather than changing unrelated code.

## 3. Modify

Use two `println!` calls or one string containing a newline. Two calls are clearer at this stage.

## 4. Build

A minimal solution is a `main` function with three `println!` calls. No variables or abstractions are needed yet.

A different implementation can also be correct. Compare behavior, clarity, and the reasoning behind your design rather than only comparing text.
