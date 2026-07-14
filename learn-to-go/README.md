# Learn Go Step by Step

This course teaches programming with Go from the beginning. You do not need programming or command-line experience.

Go is a statically typed, compiled language. The compiler checks your code and turns it into a program your computer can run. Go also includes formatting, testing, dependency, security, and profiling tools in one standard toolchain.

Complete the modules in order. Each one assumes only ideas taught earlier.

## Two ways to run the examples

### Option 1: Use the official Go Playground

Open the [Go Playground](https://go.dev/play/), replace its example with the lesson code, and select **Run**. Select **Format** to apply standard Go formatting.

The Playground is the simplest option for early modules because it runs in a browser without installation. It uses the latest stable Go release, but it is a limited sandbox. It cannot accept interactive terminal input, access arbitrary files or networks, or run long and resource-heavy programs. Playground time is also deliberately fixed. Lessons clearly say when local Go is required.

### Option 2: Work on your computer

Install a current Go release from <https://go.dev/dl/>. Core examples support Go 1.25 and newer.

Open a terminal and check the installation:

```text
go version
```

Create `main.go`, then run it with:

```text
go run main.go
```

Format and compile it with:

```text
gofmt -w main.go
go build main.go
```

The local toolchain becomes necessary for interactive input, multiple files, modules, tests, the race detector, files, networks, databases, and profiles.

## How every module is organized

Each module contains:

1. A friendly lesson in `README.md`
2. Guided work in `exercise/exercise.md`
3. A short quiz in `quiz/quiz.md`
4. Complete work in `answers/exercise/exercise-solutions.md`
5. Explained answers in `answers/quiz/quiz-answers.md`

Type examples yourself, predict their result, run them, and read the first useful compiler error before changing code.

## Course path

### First programs and decisions

- [Module 01: Use the Go Playground and Install Go](module-01-playground-install-and-run/README.md)
- [Module 02: Packages, Main, Imports, and Output](module-02-packages-main-and-output/README.md)
- [Module 03: Variables, Constants, and Basic Types](module-03-variables-constants-and-types/README.md)
- [Module 04: Numbers, Operators, and Conversions](module-04-numbers-operators-and-conversions/README.md)
- [Module 05: Strings, Bytes, Runes, and Unicode](module-05-strings-bytes-runes-unicode/README.md)
- [Module 06: Booleans, Conditions, and Switch](module-06-conditions-and-switch/README.md)
- [Module 07: Repeat Work with For and Range](module-07-loops-and-range/README.md)
- [Module 08: Read Input, Parse Text, and Format Output](module-08-input-parsing-and-output/README.md)

### Collections and program structure

- [Module 09: Arrays and Slices](module-09-arrays-and-slices/README.md)
- [Module 10: Maps](module-10-maps/README.md)
- [Module 11: Structs and Data Modeling](module-11-structs-and-data-modeling/README.md)
- [Module 12: Functions and Multiple Results](module-12-functions-and-results/README.md)
- [Module 13: Errors, Defer, Panic, and Recovery Boundaries](module-13-errors-defer-and-panic/README.md)
- [Module 14: Pointers, Values, and Mutation](module-14-pointers-values-and-mutation/README.md)
- [Module 15: Methods, Embedding, and Composition](module-15-methods-and-composition/README.md)
- [Module 16: Interfaces and Type Switches](module-16-interfaces-and-type-switches/README.md)
- [Module 17: Generics](module-17-generics/README.md)
- [Module 18: Packages, Modules, and Visibility](module-18-packages-modules-and-visibility/README.md)

### Reliable I/O and tests

- [Module 19: Files, Paths, and Streams](module-19-files-paths-and-streams/README.md)
- [Module 20: JSON and CSV Boundaries](module-20-json-and-csv/README.md)
- [Module 21: Tests with the Testing Package](module-21-testing/README.md)
- [Module 22: Benchmarks and Fuzz Tests](module-22-benchmarks-and-fuzzing/README.md)

### Concurrency without guesswork

- [Module 23: Goroutines and Lifetimes](module-23-goroutines-and-lifetimes/README.md)
- [Module 24: Channels and Select](module-24-channels-and-select/README.md)
- [Module 25: Context and Cancellation](module-25-context-and-cancellation/README.md)
- [Module 26: Synchronization and the Race Detector](module-26-synchronization-and-races/README.md)

### Services and production boundaries

- [Module 27: HTTP Clients](module-27-http-clients/README.md)
- [Module 28: HTTP Servers and Middleware](module-28-http-servers/README.md)
- [Module 29: SQL from Go](module-29-database-sql/README.md)
- [Module 30: Command-Line Programs, Configuration, and Logging](module-30-cli-config-and-logging/README.md)
- [Module 31: Dependencies, API Design, and Supply-Chain Safety](module-31-dependencies-and-api-design/README.md)
- [Module 32: Reflection](module-32-reflection/README.md)
- [Module 33: Embedded Files, Build Constraints, and Generation](module-33-embed-build-and-generate/README.md)
- [Module 34: Profiling, Optimization, and Releasing Go Programs](module-34-performance-and-release/README.md)

## Safety and study habits

Use disposable practice folders. Never use real tokens, passwords, customer records, or production databases. Treat compiler errors as guidance. Keep code formatted with `gofmt`, handle every meaningful error, and make one small change at a time.
