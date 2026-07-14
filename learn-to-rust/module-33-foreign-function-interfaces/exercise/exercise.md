# Exercise: Export a checked sum

Create a library function `sum_i32(values: *const i32, len: usize, output: *mut i64) -> i32` with the C ABI.

1. Return `1` if `output` is null.
2. Return `2` if `values` is null while `len` is not zero.
3. Otherwise sum the input and write it to `output`, then return `0`.
4. Put pointer operations in small unsafe blocks with `SAFETY` comments.
5. Document the caller's pointer and lifetime obligations. This is an advanced boundary exercise, not a recommendation to replace safe slices.
