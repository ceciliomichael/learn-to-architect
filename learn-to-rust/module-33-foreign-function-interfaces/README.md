# Module 33: Foreign Function Interfaces

An FFI boundary lets Rust exchange data with code that follows another application binary interface, commonly C. The compiler cannot verify the other language's ownership, layout, or lifetime rules, so keep this boundary small.

```rust
#[unsafe(no_mangle)]
pub extern "C" fn add(left: i32, right: i32) -> i32 {
    left + right
}
```

`extern "C"` selects the C calling convention. `no_mangle` preserves an exported symbol name and is an unsafe attribute in Rust 2024 because symbol collisions can break program safety.

Use fixed-width integers and `#[repr(C)]` structs for compatible layout. Do not pass Rust `String`, `Vec`, trait objects, or ordinary enums directly across a C ABI. C strings need `CString` or `CStr`, have a terminating zero byte, and need explicit ownership.

Never let a Rust panic unwind across an FFI boundary. Catch panics when calling user-provided Rust behavior from C and translate failures into documented error codes. Every allocation must be freed by the same allocator contract that created it. Document who owns each pointer, whether null is allowed, how long data remains valid, and which thread may call a function.

Build scripts and native libraries are platform-specific executable dependencies. Review them, isolate binding code, and test every supported target. Prefer a mature binding crate when it already maintains the difficult boundary.

Continue to [Module 34](../module-34-cargo-features-and-workspaces/README.md).
