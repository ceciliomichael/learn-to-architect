# Module 32: Unsafe Rust and Safety Contracts

## Outcome

Identify the operations unsafe Rust permits, write explicit safety invariants, keep unsafe regions small, and expose safe wrappers only when their contracts are actually enforced.

## Why this matters

Rust's safe subset deliberately rejects operations the compiler cannot prove sound. Low-level data structures, operating-system interfaces, FFI, and some performance-sensitive primitives sometimes require promises the programmer must prove manually.

## Programming concept

A safety invariant is a condition that must always hold to prevent undefined behavior, such as valid pointer alignment, initialized memory, correct length, non-overlapping mutation, or a valid lifetime. Unsafe code does not remove correctness obligations; it transfers some proof responsibility from the compiler to the programmer.

## Rust model

unsafe permits a limited set of operations including dereferencing raw pointers, calling unsafe functions, accessing union fields, using mutable statics, and implementing unsafe traits. An unsafe block is a boundary where those operations are allowed. Safe Rust rules still apply outside and around the block. Unsafe functions document caller obligations in a Safety section.

## Local Cargo example

Create cargo new unsafe_contracts --edition 2024. The example intentionally demonstrates a raw-pointer operation that should normally be written with safe indexing instead.

~~~rust
fn first_or_zero(values: &[i32]) -> i32 {
    if values.is_empty() {
        return 0;
    }

    let pointer = values.as_ptr();

    // SAFETY: values is non-empty, so pointer refers to an initialized
    // i32 at index 0. The shared slice guarantees this read is valid
    // for the duration of the borrow.
    unsafe { *pointer }
}

fn main() {
    println!("{}", first_or_zero(&[10, 20]));
    println!("{}", first_or_zero(&[]));
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- Creating a raw pointer is not by itself the dangerous operation here; dereferencing it requires unsafe.
- The preceding empty check establishes the index-0 existence invariant.
- The SAFETY comment states concrete facts rather than saying trust me.
- The function exposes a safe API because it checks the condition needed by its internal raw access.
- The safe expression values[0] or first would be better here; the raw pointer is educational only.

## Deliberate mistake

~~~rust
unsafe fn read_first(pointer: *const i32) -> i32 {
    // No stated validity, alignment, initialization, or lifetime contract.
    unsafe { *pointer }
}
~~~

The function can only be sound if callers satisfy precise pointer obligations. Marking a function unsafe is not documentation and does not make arbitrary pointers valid.

Corrected direction:

~~~rust
/// Reads one i32 from pointer.
///
/// # Safety
///
/// pointer must be non-null, properly aligned for i32, point to an
/// initialized i32 that is readable for this call, and remain valid
/// for the duration of the read.
unsafe fn read_first(pointer: *const i32) -> i32 {
    // SAFETY: The caller contract above provides the required invariants.
    unsafe { *pointer }
}
~~~

## Mental model

- unsafe means the compiler cannot prove every required invariant, not that rules disappear.
- Every unsafe operation needs a concrete proof story.
- Keep unsafe blocks as small as practical.
- A safe wrapper must validate or structurally guarantee every obligation it hides.
- Tests can find bugs but cannot prove absence of undefined behavior.
- Prefer a safe standard-library or maintained-crate abstraction when it expresses the operation.

## Common mistakes

- Using unsafe for speed without measurement.
- Writing SAFETY comments that merely restate that the code is unsafe.
- Creating a safe wrapper around an unsafe function without enforcing caller requirements.
- Assuming tests make undefined behavior acceptable.
- Spreading raw pointers throughout otherwise safe application logic.

## Transfer to other languages

C and C++ require many of these invariants throughout ordinary code; Rust isolates them behind explicit unsafe boundaries. The general engineering skill is documenting and auditing trusted code where language guarantees end.

## Guided practice

1. Replace the raw-pointer example with the safest standard-library equivalent.
2. Write a Safety section for a hypothetical function accepting pointer plus length.
3. List the invariants required by slice::from_raw_parts from its local standard-library documentation.
4. Run Clippy on a small unsafe example and inspect warnings rather than treating lint as proof.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- name common unsafe operations;
- write a concrete Safety contract;
- explain safe wrapper obligations;
- state why tests cannot prove soundness;
- prefer smaller trusted boundaries.

## Next

Continue to [Module 33](../33-foreign-function-interfaces/README.md).
