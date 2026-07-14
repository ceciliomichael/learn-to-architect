# Module 32: Unsafe Rust and Safety Contracts

`unsafe` unlocks a small set of operations the compiler cannot prove safe, including dereferencing raw pointers, calling unsafe functions, accessing mutable static data, implementing unsafe traits, and using fields of a union.

It does not turn off the borrow checker for the rest of the program. It places responsibility on the programmer to uphold rules that safe Rust normally proves.

```rust
fn first_or_zero(values: &[i32]) -> i32 {
    if values.is_empty() {
        return 0;
    }

    // SAFETY: The empty check proves index 0 is within this slice.
    unsafe { *values.as_ptr() }
}
```

This example is educational. Safe indexing is clearer and should be used here. Every real unsafe block needs a nearby `SAFETY` explanation stating concrete invariants: pointer validity, alignment, initialization, aliasing, length, lifetime, and thread rules as applicable.

Keep the unsafe block as small as possible and expose a safe wrapper only when the wrapper validates all required conditions. An unsafe function moves some obligations to its caller and must document them in a `# Safety` section.

Undefined behavior can appear to work and later fail after optimization or platform changes. Test edge cases, use Clippy, and use specialized tools such as Miri where supported. Tests increase confidence, but they cannot prove an unsafe implementation sound.

Continue to [Module 33](../module-33-foreign-function-interfaces/README.md).
