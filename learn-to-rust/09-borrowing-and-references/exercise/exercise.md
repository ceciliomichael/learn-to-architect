# Exercises: Module 09

Use a local Cargo project. Predict first.

## 1. Trace

Given let text = String::from("hi"); let a = &text; let b = &text;, identify the owner and borrowers.

## 2. Repair

Create a mutable reference, use the original value before the reference's last use, and repair the conflict by shortening or reordering the borrow.

## 3. Modify

Change length so it accepts &str instead of &String after previewing that String can be borrowed as string content.

## 4. Build

Build a small text editor model with append_word(&mut String, &str) and count_chars(&str). Keep one String owner in main and borrow it for operations.

Finish with cargo fmt, cargo clippy, and cargo check.
