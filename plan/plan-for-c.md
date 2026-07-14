# Plan for the C Learning Module

## Baseline decision

The course uses portable hosted ISO C17 as its main baseline. A newer compiler may run the checks, but examples compile with `-std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow`. C23 is taught in a late portability module after learners understand which behavior comes from the ISO language, the implementation, the operating system, or a third-party library.

The course will not contain a miscellaneous module or final assessment.

## Required structure

Every module contains `README.md`, `exercise/exercise.md`, `quiz/quiz.md`, `answers/exercise/exercise-solutions.md`, and `answers/quiz/quiz-answers.md`.

## Why this course has 35 modules

The number follows C-specific boundaries. Pointer basics, pointer bounds, and dynamic allocation remain separate because combining them creates unsafe prerequisite jumps. ABI, foreign interfaces, and libraries are grouped because they share one binary contract. Bit operations and object representation are grouped because binary interpretation must accompany bit manipulation.

## Roadmap

### Foundations

- [x] 01: Online Compiler and Local Toolchain Choices
- [x] 02: Preprocess, Compile, Link, and Run
- [x] 03: Variables, Types, Constants, and Limits
- [x] 04: Operators, Conversions, and Overflow
- [x] 05: Formatted Input and Output
- [x] 06: Conditions and Switch
- [x] 07: Loops
- [x] 08: Functions, Scope, and Header Declarations
- [x] 09: Arrays and Length Tracking
- [x] 10: Characters, Strings, and Bytes

### Memory and data modeling

- [x] 11: Pointers, Addresses, and Null
- [x] 12: Arrays, Pointer Arithmetic, and Bounds
- [x] 13: Structures and Data Ownership
- [x] 14: Enumerations, typedef, and Flags
- [x] 15: Dynamic Memory and Ownership
- [x] 16: Error Values and errno
- [x] 17: Files and Streams
- [x] 18: Preprocessor, Includes, Macros, and Generic Selection
- [x] 19: Multi-File Programs, Storage Duration, and Linkage
- [x] 20: Function Pointers and Callbacks
- [x] 21: const, volatile, restrict, and Pointer Contracts

### Correctness and builds

- [x] 22: Bits, Masks, Representation, Alignment, and Endianness
- [x] 23: Undefined, Unspecified, and Implementation-Defined Behavior
- [x] 24: Defensive Input, Size Arithmetic, and Allocation Limits
- [x] 25: Testing and Assertions
- [x] 26: Debuggers, Sanitizers, and Static Analysis
- [x] 27: Make and Repeatable Builds
- [x] 28: CMake and Installed Libraries

### Systems and production C

- [x] 29: Threads, Atomics, and Memory Ordering
- [x] 30: Networking and Platform Boundaries
- [x] 31: Libraries, ABI Contracts, and Foreign Interfaces
- [x] 32: Measure and Improve Performance
- [x] 33: Security Hardening
- [x] 34: Portability, Standards, and C23
- [x] 35: Package and Release C Programs

## Dependency order

1. No pointer arithmetic before arrays and indexes.
2. No allocation before pointer ownership and sizes.
3. No byte buffer is treated as a C string without a verified terminator.
4. No macro evaluates an argument more than documented.
5. No installed library before headers, linkage, and build tools.
6. No external length is trusted before overflow and maximum checks.
7. No platform API is presented as portable ISO C.
8. No optimization is accepted without equivalent output and measurement.

## Verification

- [x] Create all 35 modules and five required files per module
- [x] Verify browser compiler limitations and official GCC standard options
- [x] Compile standard examples as strict C17
- [x] Run representative multi-file, sanitizer, CMake, and thread builds
- [x] Check relative links, code fences, ASCII-only text, quiz counts, and unfinished markers
- [x] Update the root course catalog
- [x] Mark completed plan items

Verification used explicit C17 and C23 modes rather than the compiler default. The local Windows GCC lacks optional `threads.h` and sanitizer runtime libraries, so the C17 thread examples and UndefinedBehaviorSanitizer example were additionally run with a supporting Linux GCC environment. The installed-library CMake example was built against zlib 1.3.1.
