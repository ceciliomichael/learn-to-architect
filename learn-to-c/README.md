# Learn C Step by Step

This course teaches C from the beginning through careful systems and production work. No prior programming experience is required.

## Language baseline

Core examples use hosted ISO C17. A newer compiler is fine, but compile required examples with an explicit standard and strong warnings:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

C23 is introduced in Module 34 after portable C17 foundations. Compiler extensions and operating-system APIs are always labeled instead of being presented as ISO C.

## Online and local compilers

Early examples can run in the [Programiz C compiler](https://www.programiz.com/c-programming/online-compiler/). It is a third-party service, not an official ISO tool. Do not paste private code or data into it. Browser compilers may hide flags and restrict files, libraries, networking, debuggers, and sanitizers.

For local work, install GCC or Clang and verify the selected compiler version. Later modules use multiple files, diagnostic tools, Make, CMake, and installed libraries.

## How modules work

Each module has a lesson, guided exercise, quiz, complete exercise solution, and explained quiz answers. Follow the order carefully, especially before pointer arithmetic and dynamic allocation.

## Course path

- [Module 01: Online Compiler and Local Toolchain Choices](01-online-compiler-and-local-toolchain-choices/README.md)
- [Module 02: Preprocess, Compile, Link, and Run](02-preprocess-compile-link-and-run/README.md)
- [Module 03: Variables, Types, Constants, and Limits](03-variables-types-constants-and-limits/README.md)
- [Module 04: Operators, Conversions, and Overflow](04-operators-conversions-and-overflow/README.md)
- [Module 05: Formatted Input and Output](05-formatted-input-and-output/README.md)
- [Module 06: Conditions and Switch](06-conditions-and-switch/README.md)
- [Module 07: Loops](07-loops/README.md)
- [Module 08: Functions, Scope, and Header Declarations](08-functions-scope-and-header-declarations/README.md)
- [Module 09: Arrays and Length Tracking](09-arrays-and-length-tracking/README.md)
- [Module 10: Characters, Strings, and Bytes](10-characters-strings-and-bytes/README.md)
- [Module 11: Pointers, Addresses, and Null](11-pointers-addresses-and-null/README.md)
- [Module 12: Arrays, Pointer Arithmetic, and Bounds](12-arrays-pointer-arithmetic-and-bounds/README.md)
- [Module 13: Structures and Data Ownership](13-structures-and-data-ownership/README.md)
- [Module 14: Enumerations, typedef, and Flags](14-enumerations-typedef-and-flags/README.md)
- [Module 15: Dynamic Memory and Ownership](15-dynamic-memory-and-ownership/README.md)
- [Module 16: Error Values and errno](16-error-values-and-errno/README.md)
- [Module 17: Files and Streams](17-files-and-streams/README.md)
- [Module 18: Preprocessor, Includes, Macros, and Generic Selection](18-preprocessor-includes-macros-and-generic-selection/README.md)
- [Module 19: Multi-File Programs, Storage Duration, and Linkage](19-multi-file-programs-storage-duration-and-linkage/README.md)
- [Module 20: Function Pointers and Callbacks](20-function-pointers-and-callbacks/README.md)
- [Module 21: const, volatile, restrict, and Pointer Contracts](21-const-volatile-restrict-and-pointer-contracts/README.md)
- [Module 22: Bits, Masks, Representation, Alignment, and Endianness](22-bits-masks-representation-alignment-and-endianness/README.md)
- [Module 23: Undefined, Unspecified, and Implementation-Defined Behavior](23-undefined-unspecified-and-implementation-defined-behavior/README.md)
- [Module 24: Defensive Input, Size Arithmetic, and Allocation Limits](24-defensive-input-size-arithmetic-and-allocation-limits/README.md)
- [Module 25: Testing and Assertions](25-testing-and-assertions/README.md)
- [Module 26: Debuggers, Sanitizers, and Static Analysis](26-debuggers-sanitizers-and-static-analysis/README.md)
- [Module 27: Make and Repeatable Builds](27-make-and-repeatable-builds/README.md)
- [Module 28: CMake and Installed Libraries](28-cmake-and-installed-libraries/README.md)
- [Module 29: Threads, Atomics, and Memory Ordering](29-threads-atomics-and-memory-ordering/README.md)
- [Module 30: Networking and Platform Boundaries](30-networking-and-platform-boundaries/README.md)
- [Module 31: Libraries, ABI Contracts, and Foreign Interfaces](31-libraries-abi-contracts-and-foreign-interfaces/README.md)
- [Module 32: Measure and Improve Performance](32-measure-and-improve-performance/README.md)
- [Module 33: Security Hardening](33-security-hardening/README.md)
- [Module 34: Portability, Standards, and C23](34-portability-standards-and-c23/README.md)
- [Module 35: Package and Release C Programs](35-package-and-release/README.md)

Installed libraries are taught directly in Module 28 after headers, linkage, compiler flags, and repeatable builds. Dependency code is treated as part of the program's trust boundary.

There is intentionally no miscellaneous module or final assessment.

