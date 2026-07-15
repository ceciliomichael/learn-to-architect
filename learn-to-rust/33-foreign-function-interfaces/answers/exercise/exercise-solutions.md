# Exercise solution

```rust
/// Sums `len` signed 32-bit integers and writes the result to `output`.
///
/// # Safety
///
/// When `len` is nonzero, `values` must point to `len` initialized `i32`
/// values that remain readable for this call. `output` must point to writable,
/// properly aligned `i64` storage. The regions must satisfy Rust's aliasing rules.
#[unsafe(no_mangle)]
pub unsafe extern "C" fn sum_i32(values: *const i32, len: usize, output: *mut i64) -> i32 {
    if output.is_null() {
        return 1;
    }
    if values.is_null() && len != 0 {
        return 2;
    }

    // SAFETY: The documented caller contract makes this pointer and length a
    // readable slice. A zero-length slice accepts a non-dereferenced pointer.
    let values = unsafe { std::slice::from_raw_parts(values, len) };
    let total = values.iter().map(|value| i64::from(*value)).sum();

    // SAFETY: The documented caller contract guarantees writable i64 storage.
    unsafe { output.write(total) };
    0
}
```

The error codes handle detectable null-pointer cases. The other pointer requirements cannot be checked fully by the function, so C callers must follow the documented contract.
