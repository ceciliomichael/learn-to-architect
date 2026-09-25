# Quiz Answers: Module 33

## 1

Binary calling and layout conventions that allow separately compiled code to communicate.

## 2

Its representation and ownership semantics are Rust-specific and not a stable universal C string ABI.

## 3

Foreign code can violate pointer, lifetime, alignment, initialization, ownership, and thread assumptions the Rust compiler cannot verify.

## 4

They should be contained according to an explicitly supported strategy rather than casually unwinding into foreign code.

## 5

It converts safe Rust values into a form that satisfies the raw boundary contract, contains unsafe code, validates results, and presents normal Rust types to the rest of the program.
