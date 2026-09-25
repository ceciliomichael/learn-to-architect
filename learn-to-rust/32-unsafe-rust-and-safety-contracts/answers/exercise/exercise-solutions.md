# Exercise Solutions: Module 32

Attempt the exercises before reading.

## 1. Trace

No. unsafe only permits specific otherwise-restricted operations. Ordinary Rust checks still apply broadly.

## 2. Repair

State what pointer values are valid, for how long, with what alignment and initialization, and whether aliasing/mutation is allowed. The implementation's unsafe block should cite those established obligations.

## 3. Modify

values.first().copied().unwrap_or(0) is a safe equivalent and is preferable for this task.

## 4. Build

Validate what can be validated before entering unsafe, make uncheckable obligations part of an unsafe caller contract if necessary, perform the minimum raw operation, and return to safe types immediately.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
