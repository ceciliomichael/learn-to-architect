# Exercise Solutions: Module 17

Attempt the exercises before reading.

## 1. Trace

lib.rs is the library crate root and main.rs is the binary crate root.

## 2. Repair

Provide public construction and methods that preserve the field invariant rather than making the field public.

## 3. Modify

Declare the helper without pub so public code can use it internally without exporting its name.

## 4. Build

Organize around responsibilities and invariants. Avoid making every type or field public merely for convenience.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
