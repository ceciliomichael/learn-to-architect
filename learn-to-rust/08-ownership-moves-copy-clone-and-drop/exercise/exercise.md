# Exercises: Module 08

Use a local Cargo project. Predict first.

## 1. Trace

For let a = String::from("x"); let b = a; identify the owner before and after the assignment.

## 2. Repair

Try to print both a and b after that move. Repair it without cloning, then explain when cloning would instead be justified.

## 3. Modify

Write consume(text: String) that prints text. Call it and observe whether the caller can use the String afterward.

## 4. Build

Build a small program that creates three owned Strings, moves one into a function, clones one for a genuinely independent copy, and leaves one untouched. Comment each ownership transition.

Finish with cargo fmt, cargo clippy, and cargo check.
