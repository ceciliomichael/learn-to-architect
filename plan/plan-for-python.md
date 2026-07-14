# Plan for the Python Learning Module

## Purpose

This document tracks `python-learning-module/`, a complete beginner-to-advanced Python course for learners with no programming background.

The runnable core targets Python 3.12 and newer. The writing is checked against the current stable Python documentation, and any feature needing a later version must be labeled. The course does not include a miscellaneous module or a final assessment.

## Findings that shape the course

Many beginner Python paths move too quickly from printing text to compact comprehensions and classes. They often leave learners confused about names, objects, mutation, errors, modules, and environments. Advanced paths then assume testing, typing, file safety, concurrency, and package structure without building those foundations.

This course will correct that by:

1. Teaching scripts and error reading before asking learners to build programs.
2. Separating number, text, and conversion behavior.
3. Teaching conditions before loops and loops before collections shortcuts.
4. Teaching names, object identity, and mutation before advanced function or class behavior.
5. Teaching ordinary functions before compact comprehensions, decorators, or generators.
6. Teaching exceptions before file and external-data work.
7. Teaching modules before packages, environments, and dependencies.
8. Teaching type hints and ordinary classes before class-based tests, advanced typing, and larger designs.
9. Treating type hints as static information, not runtime enforcement.
10. Separating threads, processes, and async I/O by the kind of work each solves.

## Required module structure

```text
module-NN-topic/
  README.md
  exercise/
    exercise.md
  quiz/
    quiz.md
  answers/
    exercise/
      exercise-solutions.md
    quiz/
      quiz-answers.md
```

Every lesson uses plain language, no emoji, and no em dash characters. Exercises are complete and repeatable. Answers explain reasoning and expected behavior.

## Planned course sequence

### Part 1: First programs and decisions

- [x] **Module 01: Install Python and Run a Program**
  - Interpreter, terminal, version check, REPL, scripts, working folders, comments, indentation, and reading tracebacks.
- [x] **Module 02: Values, Variables, and Types**
  - Objects, names, assignment, `print`, `type`, `None`, naming, and reassignment.
- [x] **Module 03: Numbers and Arithmetic**
  - Integers, floats, arithmetic, precedence, division forms, rounding limitations, and `decimal` preview.
- [x] **Module 04: Text and String Operations**
  - Unicode strings, quotes, escapes, length, indexing, slicing, immutability, methods, and f-strings.
- [x] **Module 05: Input and Conversion**
  - `input`, string results, `int` and `float`, conversion failure, clear prompts, and why retry handling waits for later control-flow lessons.
- [x] **Module 06: Booleans and Conditions**
  - Comparisons, `and`, `or`, `not`, truth values, `if`, `elif`, `else`, membership, identity, and parentheses.
- [x] **Module 07: Repeat with While Loops**
  - Loop state, termination, `break`, `continue`, and avoiding infinite loops.
- [x] **Module 08: Repeat with For and Range**
  - Iteration, `range`, `enumerate`, `zip`, loop `else`, and choosing loop type.

### Part 2: Work with collections

- [x] **Module 09: Lists and Mutation**
  - Creation, indexing, slicing, methods, copying, aliasing, nested lists, and mutation during iteration.
- [x] **Module 10: Tuples and Unpacking**
  - Immutability, packing, unpacking, swapping, starred targets, and fixed records.
- [x] **Module 11: Dictionaries**
  - Key-value modeling, lookup, updates, safe access, iteration, ordering guarantee, and nested data.
- [x] **Module 12: Sets and Membership**
  - Uniqueness, set algebra, mutable and frozen sets, hashability, and use cases.

### Part 3: Build dependable functions

- [x] **Module 13: Define and Call Functions**
  - `def`, parameters, return values, returning related tuple values, `None`, docstrings, decomposition, and pure behavior.
- [x] **Module 14: Use Parameters Clearly**
  - Positional and keyword arguments, defaults, keyword-only and positional-only syntax, `*args`, `**kwargs`, and mutable default trap.
- [x] **Module 15: Names, Scope, Objects, and Mutation**
  - LEGB lookup, local and global names, identity, aliasing, argument passing, copying, and controlled side effects.
- [x] **Module 16: Comprehensions and Generator Expressions**
  - List, set, and dictionary comprehensions, filters, readable limits, and lazy generator expressions.

### Part 4: Errors, files, and reusable code

- [x] **Module 17: Handle Exceptions Deliberately**
  - Exception types, `try`, `except`, `else`, `finally`, built-in errors, chaining, and narrow handling.
- [x] **Module 18: Read and Write Files with pathlib**
  - Paths, encodings, context management, text and bytes, safe replacement, and filesystem errors.
- [x] **Module 19: Work with JSON and CSV Data**
  - Serialization, schema validation, untrusted input, JSON limitations, CSV newline handling, and round trips.
- [x] **Module 20: Modules, Imports, and Packages**
  - Import behavior, `__name__`, main guard, module search, package layout, absolute imports, and avoiding circular imports.
- [x] **Module 21: Virtual Environments and Dependencies**
  - `venv`, activation, interpreter selection, pip through `python -m`, requirements, lock concepts, and dependency trust.

### Part 5: Add type information

- [x] **Module 22: Add Type Hints**
  - Built-in generic types, unions, optionals, callable signatures, `TypeAlias`, narrowing, and runtime boundary validation.

### Part 6: Model behavior with objects

- [x] **Module 23: Classes and Instances**
  - Class creation, `self`, instance attributes, methods, class attributes, invariants, custom exception classes, and encapsulation conventions.
- [x] **Module 24: Test with unittest**
  - Arrange-act-assert, test discovery, assertions, fixtures, boundaries, exceptions, and test isolation.
- [x] **Module 25: Protocols, Generics, and Typed Data**
  - Type variables, generic functions and classes, protocols, `TypedDict`, `Literal`, `NewType`, and variance intuition.
- [x] **Module 26: Dataclasses and Enums**
  - Generated methods, default factories, frozen behavior, slots tradeoffs, enums, and value objects.
- [x] **Module 27: Composition and Inheritance**
  - Has-a compared with is-a, overriding, `super`, abstract base classes, protocols, multiple inheritance caution, and Liskov-style substitutability.
- [x] **Module 28: Python's Data Model**
  - `repr`, equality, ordering, hashing, containment, callability, properties, descriptors at an introductory advanced level, and operator overloading restraint.

### Part 7: Lazy work and managed behavior

- [x] **Module 29: Iterators and Generators**
  - Iterable protocol, iterator state, `iter`, `next`, `yield`, generator cleanup, `yield from`, and single-use behavior.
- [x] **Module 30: Closures and Decorators**
  - First-class functions, closures, `nonlocal`, decorators, `functools.wraps`, decorator factories, and transparent wrappers.
- [x] **Module 31: Context Managers**
  - `with`, enter and exit protocol, cleanup, `contextlib.contextmanager`, `ExitStack`, and exception suppression caution.

### Part 8: Practical standard library and data access

- [x] **Module 32: Dates, Time Zones, Decimal, and Randomness**
  - Aware datetimes, `zoneinfo`, durations, exact decimal contexts, ordinary random compared with `secrets`, and reproducibility.
- [x] **Module 33: Use SQLite Safely from Python**
  - Connections, transactions, parameter binding, row factories, context behavior, schema setup, and injection prevention.
- [x] **Module 34: Logging, Configuration, and Command-Line Programs**
  - `logging`, structured context, log levels, secret redaction, environment configuration, `argparse`, exit codes, and stderr.

### Part 9: Concurrency and performance

- [x] **Module 35: Threads, Processes, and Queues**
  - I/O-bound and CPU-bound work, thread safety, locks, futures, process serialization, queues, cancellation, and shutdown.
- [x] **Module 36: Async I/O with asyncio**
  - Coroutines, event loop, tasks, structured waiting, timeouts, cancellation, blocking calls, synchronization, and async context managers.
- [x] **Module 37: Debug, Profile, and Improve Performance**
  - Tracebacks, debugger, assertions, timing, profiling, memory behavior, algorithmic complexity, caching, and measurement discipline.

### Part 10: Ship maintainable Python

- [x] **Module 38: Project Structure, Packaging, and Secure Boundaries**
  - `pyproject.toml`, source layout, public API, resources, versioning, build artifacts, environment secrets, input boundaries, subprocess safety, dependency review, and maintainable architecture.

## Dependency rules

1. No loop appears before its control flow is explained.
2. No compact comprehension appears before ordinary loops and collections.
3. No mutable default appears without explaining object reuse.
4. No file example omits encoding or cleanup reasoning.
5. No external input is trusted without validation.
6. No import assumes a package layout not yet taught.
7. No type hint is described as runtime validation.
8. No inheritance appears before instance and composition behavior.
9. No decorator appears before first-class functions and closures.
10. No concurrency example mutates shared state without explaining synchronization.
11. No SQL example constructs statements from user text.
12. No performance claim is accepted without a measurement method.

## Version strategy

- All core examples run on Python 3.12 and newer.
- Use `list[str]`, `X | None`, `pathlib`, `zoneinfo`, dataclasses, and modern `asyncio` APIs supported by that baseline.
- Do not use Python 3.14-only syntax in baseline exercises.
- Current documentation can be cited for concepts while version availability is stated accurately.

## Estimated focused learning time

The course represents about 125 to 195 focused hours:

- Lessons and typed examples: 50 to 75 hours
- Exercises and debugging: 55 to 85 hours
- Quizzes, repetition, and review: 20 to 35 hours

## Implementation checklist

- [x] Verify the version strategy against current official Python documentation
- [x] Define the ordered beginner-to-advanced path
- [x] Create the Python course root guide
- [x] Create Modules 01 to 08
- [x] Create Modules 09 to 16
- [x] Create Modules 17 to 24
- [x] Create Modules 25 to 31
- [x] Create Modules 32 to 38
- [x] Verify every required folder and file
- [x] Check every relative Markdown link
- [x] Scan for emoji, em dash characters, placeholders, and unbalanced fences
- [x] Compile all baseline Python code blocks where appropriate
- [x] Execute representative end-to-end examples on Python 3.12
- [x] Update the repository root README
- [x] Mark every roadmap item complete

## Definition of done

The course is complete when all 38 modules exist in the required organization, all baseline examples are valid on Python 3.12, every topic follows its prerequisites, unsafe boundary examples are clearly rejected, exercises and answers are complete, links and formatting pass audits, and the repository root recommends the course to beginners.
