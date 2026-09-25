# Exercises: Module 32

Work locally and explain your choices.

## 1. Trace

Does placing code inside unsafe disable the borrow checker for all surrounding Rust?

## 2. Repair

Take an unsafe function with an undocumented raw pointer and add a precise caller Safety contract plus a local SAFETY comment.

## 3. Modify

Rewrite first_or_zero entirely in safe Rust using first and copied or pattern matching.

## 4. Build

Design, but do not over-engineer, a safe function wrapping an unsafe pointer-plus-length operation. Document exactly where null, alignment, initialization, lifetime, and length assumptions are established.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
