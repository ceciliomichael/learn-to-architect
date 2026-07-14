# Plan for the Go Learning Module

## Purpose

This document tracks `learn-to-go/`, a beginner-to-advanced Go course for learners with no programming experience.

The course begins in the official Go Playground, then moves to the local Go toolchain when learners need files, packages, modules, tests, the race detector, networking, databases, and profiling. Core examples target Go 1.25 and newer so they work with the installed Go 1.25.4 compiler while remaining valid on the current stable release.

The course will not contain a miscellaneous module or final assessment.

## Teaching decisions

1. Explain compilation, packages, and `main` before adding language syntax.
2. Teach strings before slices, while clearly delaying slice mechanics.
3. Teach conditions before loops and loops before mutable collections.
4. Teach structs and functions before methods and interfaces.
5. Teach ordinary concrete code before generics.
6. Teach explicit errors before file, network, and database boundaries.
7. Teach tests before concurrency and production I/O.
8. Teach goroutines before channels, channels before cancellation, and cancellation before shared-state synchronization.
9. Use only parameterized SQL and bounded external input.
10. Require measurements before performance claims.

## Required module structure

```text
module-NN-topic/
|-- README.md
|-- exercise/
|   `-- exercise.md
|-- quiz/
|   `-- quiz.md
`-- answers/
    |-- exercise/
    |   `-- exercise-solutions.md
    `-- quiz/
        `-- quiz-answers.md
```

Every lesson uses plain language, no emoji, and no em dash characters. Exercises are repeatable and their answers are complete.

## Course roadmap

### Part 1: First programs and decisions

- [x] **Module 01: Use the Go Playground and Install Go**
  - Official Playground, sandbox limits, installation, `go version`, files, `go run`, `go build`, formatting, and compiler messages.
- [x] **Module 02: Packages, Main, Imports, and Output**
  - `package main`, `func main`, imports, `fmt`, statements, comments, exported names, and unused-name errors.
- [x] **Module 03: Variables, Constants, and Basic Types**
  - `var`, short declarations, zero values, constants, static types, inference, scope preview, and meaningful names.
- [x] **Module 04: Numbers, Operators, and Conversions**
  - Integer and float types, arithmetic, division, overflow awareness, precedence, explicit conversions, and exact-money caution.
- [x] **Module 05: Strings, Bytes, Runes, and Unicode**
  - UTF-8 strings, byte length, runes, indexing limitations, raw strings, escapes, and safe iteration preview.
- [x] **Module 06: Booleans, Conditions, and Switch**
  - Comparisons, logical operators, `if`, initializer statements, `else`, expression and condition switches, and branch order.
- [x] **Module 07: Repeat Work with For and Range**
  - Go's single loop form, conditions, classic clauses, `range`, `break`, `continue`, termination, and loop variables.
- [x] **Module 08: Read Input, Parse Text, and Format Output**
  - `bufio.Scanner`, `os.Stdin`, `strings`, `strconv`, parsing failures, clear prompts, retry loops, and formatted output.

### Part 2: Collections and program structure

- [x] **Module 09: Arrays and Slices**
  - Fixed arrays, slice views, length, capacity, append, copy, nil and empty slices, aliasing, and safe iteration.
- [x] **Module 10: Maps**
  - Creation, lookup, comma-ok, insertion, deletion, nil maps, unordered iteration, copying, and set modeling.
- [x] **Module 11: Structs and Data Modeling**
  - Fields, literals, zero values, nesting, equality limits, tags preview, and choosing clear domain data.
- [x] **Module 12: Functions and Multiple Results**
  - Parameters, results, multiple returns, named-result restraint, variadic parameters, first-class functions, closures, and decomposition.
- [x] **Module 13: Errors, Defer, Panic, and Recovery Boundaries**
  - Error values, wrapping, inspection, sentinels, `defer`, panic meaning, and narrow recovery.
- [x] **Module 14: Pointers, Values, and Mutation**
  - Addresses, dereferencing, value copies, pointer parameters, nil, escape behavior at a useful level, and mutation contracts.
- [x] **Module 15: Methods, Embedding, and Composition**
  - Value and pointer receivers, method sets, embedding, promotion, composition, invariants, and avoiding inheritance thinking.
- [x] **Module 16: Interfaces and Type Switches**
  - Implicit satisfaction, small consumer-owned interfaces, custom error types, nil interface traps, type assertions, type switches, and boundary design.
- [x] **Module 17: Generics**
  - Type parameters, constraints, `comparable`, generic functions and types, inference, and when concrete code is clearer.
- [x] **Module 18: Packages, Modules, and Visibility**
  - Package responsibilities, module paths, `go.mod`, imports, internal packages, `init` restraint, documentation, and cycles.

### Part 3: Reliable I/O and tests

- [x] **Module 19: Files, Paths, and Streams**
  - `os`, `io`, `bufio`, `path/filepath`, permissions, cleanup, bounded reads, atomic replacement, and filesystem errors.
- [x] **Module 20: JSON and CSV Boundaries**
  - Encoding, decoding, struct tags, unknown fields, validation, streaming, CSV records, size limits, and untrusted data.
- [x] **Module 21: Tests with the Testing Package**
  - Test files, table-driven tests, subtests, helpers, temporary directories, examples, integration boundaries, and coverage limits.
- [x] **Module 22: Benchmarks and Fuzz Tests**
  - Benchmarks, allocations, representative workloads, fuzz seeds, properties, regression corpus, and bounded fuzz runs.

### Part 4: Concurrency without guesswork

- [x] **Module 23: Goroutines and Lifetimes**
  - Starting work, scheduling, waiting, captured variables, observing failures, ownership, and avoiding leaked goroutines.
- [x] **Module 24: Channels and Select**
  - Send and receive, buffered and unbuffered channels, closing ownership, ranging, `select`, timeouts, and pipeline shutdown.
- [x] **Module 25: Context and Cancellation**
  - Cancellation signals, deadlines, request-scoped values, propagation, cleanup, and why context is not optional configuration.
- [x] **Module 26: Synchronization and the Race Detector**
  - Mutexes, read-write locks, once, atomics at a careful level, wait groups, data races, memory visibility, and `go test -race`.

### Part 5: Services and production boundaries

- [x] **Module 27: HTTP Clients**
  - Requests, context, client reuse, timeouts, status handling, body limits, JSON validation, URL safety, and cleanup.
- [x] **Module 28: HTTP Servers and Middleware**
  - Handlers, routing, request limits, responses, middleware, server timeouts, graceful shutdown, and `httptest`.
- [x] **Module 29: SQL from Go**
  - `database/sql`, drivers, connection pools, parameter binding, row cleanup, transactions, nulls, context, and injection prevention.
- [x] **Module 30: Command-Line Programs, Configuration, and Logging**
  - `flag`, arguments, environment configuration, validation, `log/slog`, secret-safe events, exit codes, stdout, and stderr.
- [x] **Module 31: Dependencies, API Design, and Supply-Chain Safety**
  - Minimal dependencies, module versions, `go mod tidy`, verification, vulnerability checks, public compatibility, and review.
- [x] **Module 32: Reflection**
  - Runtime type information, addressability, tags, safe inspection, performance costs, and preferring ordinary typed code.
- [x] **Module 33: Embedded Files, Build Constraints, and Generation**
  - `embed`, build constraints, platform files, `go generate`, reproducibility, generated-code review, and cross-compilation.
- [x] **Module 34: Profiling, Optimization, and Releasing Go Programs**
  - CPU and heap profiles, tracing overview, allocations, compiler diagnostics, build information, reproducible releases, and operational security.

## Dependency rules

1. No loop appears before conditions.
2. No slice mutation appears before aliasing is explained.
3. No method appears before structs and functions.
4. No interface appears before methods.
5. No generic abstraction appears before concrete equivalents.
6. No ignored error appears in successful example code.
7. No goroutine exercise exits without a defined completion policy.
8. No channel is closed by a receiver that does not own sending.
9. No network call lacks a timeout and bounded response policy.
10. No SQL statement inserts external text into query syntax.
11. No secret or private record is logged.
12. No performance conclusion is made without repeatable evidence.

## Verification checklist

- [x] Confirm current official Go guidance and Playground behavior
- [x] Create the Go root README with online and local options
- [x] Create Modules 01 through 08
- [x] Create Modules 09 through 18
- [x] Create Modules 19 through 26
- [x] Create Modules 27 through 34
- [x] Verify all required folders and files
- [x] Check every relative Markdown link
- [x] Check code fences, ASCII-only writing, and unfinished markers
- [x] Format all complete Go examples with `gofmt`
- [x] Compile all complete Go examples that can run independently
- [x] Run representative tests, fuzz seeds, race checks, HTTP, and database examples
- [x] Update the repository root README
- [x] Mark every roadmap item complete

## Definition of done

The course is complete when all 34 modules exist in the required structure, beginner examples work in the official Playground where stated, local examples work with Go 1.25.4 and current Go releases, prerequisites remain ordered, exercises have complete answers, unsafe boundaries are rejected clearly, and all repository audits pass.
