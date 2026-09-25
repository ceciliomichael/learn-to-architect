# Exercises: Module 13

Use a local Cargo project. Predict first.

## 1. Trace

What are the possible values of Option<u32>, conceptually? Is Some(0) the same as None?

## 2. Repair

Write a function that directly indexes the first element of possibly empty input. Change its return type to Option and remove the panic.

## 3. Modify

Change first_even so it returns the position of the first even value as Option<usize>.

## 4. Build

Create find_name(names: &[&str], target: &str) -> Option<usize> and print a clear found/not-found message in main.

Finish with cargo fmt, cargo clippy, and cargo check.
