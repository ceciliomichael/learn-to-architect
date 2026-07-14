# Quiz answers

1. It selects the C calling convention.
2. It requests a C-compatible field layout.
3. No. Use an explicitly documented string representation and ownership contract.
4. Memory should be released through the allocator contract that created it, often through a matching library free function.
5. Unwinding into code that does not understand Rust panics can cause undefined behavior.
