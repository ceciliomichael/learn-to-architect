# Exercises: Module 28

Work locally and explain your choices.

## 1. Trace

If one Rc has two additional Rc::clone owners, how many strong owners exist before any are dropped?

## 2. Repair

Try to move Rc<String> into thread::spawn and replace it with Arc while preserving ownership in the original thread.

## 3. Modify

Store Box<List> recursively and add a function that computes the list length by borrowing.

## 4. Build

Model a single-threaded tree where children are strongly owned but an optional parent link uses Weak. Explain how this avoids a strong cycle.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
