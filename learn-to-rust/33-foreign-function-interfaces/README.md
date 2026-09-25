# Module 33: Foreign Function Interfaces

## Outcome

Explain ABI boundaries, use C-compatible function signatures and raw pointers, define ownership and error contracts across languages, and wrap unsafe FFI behind safer Rust APIs.

## Why this matters

Systems rarely live in one language forever. Rust may call operating-system APIs or C libraries, or expose functions to C, C++, mobile, embedded, or other runtimes. At that boundary Rust's ordinary type and lifetime guarantees cannot automatically extend into foreign code.

## Programming concept

An ABI defines binary-level calling conventions and data-layout expectations. Cross-language boundaries require explicit agreements about ownership, allocation, strings, buffers, error reporting, thread use, and who may call what after what lifetime ends.

## Rust model

extern "C" selects the C calling convention for interoperable functions. repr(C) requests C-compatible layout for supported data structures. Raw pointers and C string types are common because references and String are Rust-specific abstractions. Rust 2024 treats certain FFI-related attributes and declarations as explicitly unsafe because symbol/export and foreign-call contracts carry obligations.

## Local Cargo example

Create cargo new ffi_boundaries --edition 2024. This example simulates a C-callable boundary inside one Rust binary so you can study the contract without first configuring an external C build.

~~~rust
use std::slice;

/// Sums len i32 values starting at pointer.
///
/// # Safety
///
/// If len is greater than zero, pointer must be non-null, properly
/// aligned for i32, and point to len initialized readable i32 values.
/// The memory must remain valid for the duration of this call.
#[unsafe(no_mangle)]
pub unsafe extern "C" fn sum_i32(pointer: *const i32, len: usize) -> i64 {
    let values: &[i32] = if len == 0 {
        &[]
    } else {
        // SAFETY: Required by the public unsafe function contract.
        unsafe { slice::from_raw_parts(pointer, len) }
    };

    values.iter().map(|&value| i64::from(value)).sum()
}

fn safe_sum(values: &[i32]) -> i64 {
    // SAFETY: A Rust slice supplies a valid pointer, exact length,
    // initialized readable elements, and a lifetime covering the call.
    unsafe { sum_i32(values.as_ptr(), values.len()) }
}

fn main() {
    println!("{}", safe_sum(&[10, 20, 30]));
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- extern C defines the calling convention expected by a C-compatible caller.
- The exported symbol attribute is marked unsafe in Rust 2024 because symbol naming participates in global linker contracts.
- The foreign-facing function uses pointer plus length instead of a Rust slice in its ABI.
- The unsafe function states caller obligations that foreign code must honor.
- safe_sum reconstructs those obligations from a safe Rust slice and keeps the rest of the application in safe Rust.

## Deliberate mistake

~~~rust
#[unsafe(no_mangle)]
pub extern "C" fn first(pointer: *const i32) -> i32 {
    unsafe { *pointer }
}
~~~

The public function is safe to call from Rust even though it dereferences an arbitrary foreign pointer. A safe caller could pass null or invalid memory and trigger undefined behavior. The signature hides obligations that it cannot guarantee.

Corrected direction:

~~~rust
/// # Safety
///
/// pointer must be non-null, aligned, initialized, readable, and
/// valid for one i32 read during the call.
#[unsafe(no_mangle)]
pub unsafe extern "C" fn first(pointer: *const i32) -> i32 {
    unsafe { *pointer }
}
~~~

## Mental model

- Treat FFI as an untrusted type-system boundary.
- Use C-compatible representations, not Rust-specific layout assumptions.
- Document allocation and deallocation ownership explicitly.
- Never let foreign code guess whether a pointer is borrowed or owned.
- Define error transport without unwinding assumptions; do not let Rust panics casually cross an FFI boundary.
- Wrap foreign interfaces in a narrow Rust module that converts into safe domain types quickly.

## Common mistakes

- Passing String, Vec, or ordinary Rust references as if their ABI were a stable C contract.
- Freeing memory in a different allocator than the one that created it without an explicit compatible contract.
- Returning borrowed pointers whose owners have already been destroyed.
- Allowing panics to cross an ABI boundary without a carefully documented supported mechanism.
- Using repr(C) and assuming that alone makes every nested field universally interoperable.

## Transfer to other languages

Every language interop system needs an ABI or marshaling contract. JNI, Swift/C bridging, Python C extensions, .NET P/Invoke, WebAssembly host interfaces, and native mobile bridges all require explicit lifetime and representation agreements.

## Guided practice

1. Write a repr(C) struct using fixed-width numeric fields and explain each field's cross-language meaning.
2. Convert a Rust slice to pointer plus length for a controlled unsafe call.
3. Write down who owns a returned buffer in a hypothetical C API.
4. Study CString and CStr for NUL-terminated C text and list how that differs from Rust String.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- explain ABI versus high-level type API;
- state pointer/length safety obligations;
- use a narrow unsafe extern boundary;
- describe ownership and error contracts that foreign callers need;
- wrap FFI into safe Rust quickly.

## Next

Continue to [Module 34](../34-threads-and-scoped-threads/README.md).
