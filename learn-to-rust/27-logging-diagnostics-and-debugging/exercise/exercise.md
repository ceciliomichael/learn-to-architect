# Exercises: Module 27

Work locally and explain your choices.

## 1. Trace

Why should a lower-level function often return an error instead of both logging it and returning it?

## 2. Repair

Remove a secret value from a log statement while preserving non-sensitive context useful for diagnosis.

## 3. Modify

Add a request_id string argument to process_item and include it as a tracing field.

## 4. Build

Create a small batch processor with one span per batch and structured events for item success/failure. Return errors to the caller and log each failure only at the boundary that owns operational context.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
