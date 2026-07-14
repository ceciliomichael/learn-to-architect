# Exercise: Wrap unchecked slice access

Write `get_checked(values: &[i32], index: usize) -> Option<i32>`.

1. Return `None` when the index is outside the slice.
2. For a valid index, use `get_unchecked` inside one small unsafe block.
3. Add a `SAFETY` comment explaining why the operation is valid.
4. Test an empty slice, the first value, the last value, and an invalid index.
5. Explain why ordinary `values.get(index).copied()` is preferable in production.
