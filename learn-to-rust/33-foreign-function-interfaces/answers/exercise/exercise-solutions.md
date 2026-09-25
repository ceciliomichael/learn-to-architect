# Exercise Solutions: Module 33

Attempt the exercises before reading.

## 1. Trace

A Rust slice is a Rust language abstraction whose ABI is not the portable C pointer type contract. Pointer plus length expresses the required representation explicitly for C-style interfaces.

## 2. Repair

The raw-pointer function must be unsafe because callers provide the validity proof. A safe wrapper can accept &[T], derive pointer/length from it, and contain the unsafe call.

## 3. Modify

Map None to a contract such as null pointer plus zero length only if the FFI API explicitly permits that combination. Some raw slice constructors require special non-null rules even at zero length, so keep the representation contract precise.

## 4. Build

Write the ABI contract first. A robust design makes ownership direction and errors explicit, avoids exceptions/panics crossing the boundary, and converts raw inputs into validated internal data as early as possible.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
