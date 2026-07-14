# Exercise: Count calls through shared access

Create `CallCounter` with a `Cell<u32>` field.

1. Add `new`, `record(&self)`, and `count(&self)` methods.
2. Call `record` three times through one immutable binding.
3. Print the result.
4. Add a short comment explaining why `Cell<u32>` works here.
5. Do not use `mut`, `unsafe`, or global state.
