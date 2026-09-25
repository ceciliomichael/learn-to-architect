# Exercises: Module 14

Use a local Cargo project. Predict first.

## 1. Trace

For a function returning Result<u32, String>, list the two possible variant shapes and what ? does when it sees each.

## 2. Repair

Replace a parse().unwrap() on user text with a Result-returning function and handle the failure in main.

## 3. Modify

Extend parse_positive with a maximum accepted value and return a distinct message when the number is too large.

## 4. Build

Build parse_port(text: &str) -> Result<u16, String>. Reject invalid numbers and port 0 with useful context, then let main print either the accepted port or one error message.

Finish with cargo fmt, cargo clippy, and cargo check.
