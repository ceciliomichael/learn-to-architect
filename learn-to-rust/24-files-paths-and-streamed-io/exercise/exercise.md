# Exercises: Module 24

Work locally and explain your choices.

## 1. Trace

Why can reader.lines() be preferable to read_to_string for a multi-gigabyte log?

## 2. Repair

Replace unwrap on File::open with a Result-returning function and one reporting boundary.

## 3. Modify

Change the example to count non-empty lines instead of printing them.

## 4. Build

Build a log_summary tool that accepts a Path, streams lines, counts total/empty/error-tagged lines, and returns a summary struct. Keep the counting logic testable without a real file.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
