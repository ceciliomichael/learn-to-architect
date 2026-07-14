# Plan for the Java Learning Module

## Baseline decision

The course targets Java 21 and newer. Java 21 is an established long-term-support release and contains the modern features this curriculum needs without preview flags: records, sealed classes, switch expressions, record patterns, pattern matching for switch, and virtual threads.

Development may use a newer JDK, but course examples must compile with `javac --release 21`. Java 25-specific or later features are optional notes only. This keeps the curriculum useful across current LTS installations instead of mirroring one development machine.

The course will not contain a miscellaneous module or final assessment.

## Required structure

Every module contains `README.md`, `exercise/exercise.md`, `quiz/quiz.md`, `answers/exercise/exercise-solutions.md`, and `answers/quiz/quiz-answers.md`.

## Why this course has 40 modules

The number follows the content boundaries below. Equality and hashing need their own module because collections depend on them. Installed dependencies need a separate module because build tools, version resolution, and supply-chain trust are larger than package syntax. Virtual threads remain separate from shared-state synchronization because task scale and data-race safety are different problems.

## Roadmap

### Foundations

- [x] 01: Playground, JDK Choices, and Tool Versions
- [x] 02: Source Files, Compilation, Class Files, and Main
- [x] 03: Variables, Primitive Types, and Constants
- [x] 04: Strings, Characters, Unicode, and Text Blocks
- [x] 05: Operators, Conversions, Overflow, and Math
- [x] 06: Conditions and Switch Expressions
- [x] 07: Loops and Repetition
- [x] 08: Methods, Parameters, Return Values, and Scope
- [x] 09: Arrays and Command-Line Arguments
- [x] 10: Console Input, Parsing, and Validation

### Modeling and reusable behavior

- [x] 11: Classes and Objects
- [x] 12: Constructors, Encapsulation, and Invariants
- [x] 13: Immutability and Records
- [x] 14: Enums, Sealed Types, and Pattern Matching
- [x] 15: Exceptions and Resource Cleanup
- [x] 16: Lists, Sets, and Maps
- [x] 17: Generics and Type Bounds
- [x] 18: Interfaces and Composition
- [x] 19: Inheritance and Polymorphism
- [x] 20: Equality, Hashing, and Ordering
- [x] 21: Lambdas and Functional Interfaces
- [x] 22: Streams and Optional Values

### Program structure and external boundaries

- [x] 23: Packages, Access, Classpaths, Modules, and JARs
- [x] 24: Files, Paths, and Buffered I/O
- [x] 25: Date, Time, Locale, and Formatting
- [x] 26: Regular Expressions and Text Processing
- [x] 27: Maven, Gradle, and Installed Dependencies
- [x] 28: Testing with JUnit
- [x] 29: JSON and Untrusted Data
- [x] 30: HTTP Clients and Network Boundaries
- [x] 31: JDBC, Connection Pools, and Transactions

### Concurrent and production Java

- [x] 32: Threads, Executors, Futures, and Task Completion
- [x] 33: Virtual Threads and Task Ownership
- [x] 34: Synchronization and Concurrent Collections
- [x] 35: Reflection, Annotations, and Runtime Types
- [x] 36: JVM Memory, Garbage Collection, and Resource Ownership
- [x] 37: Measurement, JFR, and JMH
- [x] 38: Command-Line Configuration and Logging
- [x] 39: Documentation, API Compatibility, and Dependency Security
- [x] 40: Build, Package, and Release Java Programs

## Dependency order

1. No class design before values, methods, arrays, and input are understood.
2. No collection shortcut before arrays and references are explained.
3. No generic bound before concrete collection use.
4. No stream pipeline before loops, collections, lambdas, and Optional.
5. No installed library before packages, JARs, classpaths, and build inputs are explained.
6. No HTTP or database value is trusted merely because parsing succeeded.
7. No concurrent task is started without a completion, cancellation, or shutdown owner.
8. No performance claim comes from one cold or debug-only run.

## Verification

- [x] Create all 40 modules and five required files per module
- [x] Verify official Playground and Java 21 language guidance
- [x] Compile standard examples with `javac --release 21 -Xlint:all`
- [x] Run representative JUnit and dependency-backed examples
- [x] Check relative links, code fences, ASCII-only text, quiz counts, and unfinished markers
- [x] Update the root course catalog
- [x] Mark completed plan items

Verification used JDK 25 only as the host compiler. Required source was compiled with `--release 21`, including the standard JDBC boundary. JUnit 6.1.2 tests and the Jackson 3.1.3 example were also resolved and built with Maven while retaining the Java 21 release target.
