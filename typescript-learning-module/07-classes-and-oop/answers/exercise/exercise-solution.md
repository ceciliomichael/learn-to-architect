# Module 07 Exercise Solutions: Architectural Overview

This document serves as the master architectural guide and reference index for all practical coding challenges in Module 07 (Classes and Object-Oriented Programming). 

In enterprise software development, Object-Oriented Programming is not merely a syntax choice; it is a foundational paradigm for organizing complex domain logic into self-contained, maintainable, and secure components. Below is the architectural summary of how each challenge reinforces production-grade engineering principles.

## Challenge Index & Solution Guides

1. **[Challenge 01 Solution: Secure Bank Account](./challenge-01-solution.md)**: Demonstrates encapsulation, data privacy using access modifiers (`private`, `readonly`, `public`), and boundary validation.
2. **[Challenge 02 Solution: Inheritance and super](./challenge-02-solution.md)**: Demonstrates class hierarchies, constructor delegation via `super()`, method overriding, and parameter property shorthand.
3. **[Challenge 03 Solution: Abstract Classes and Interfaces](./challenge-03-solution.md)**: Demonstrates contract enforcement, polymorphic design, and the distinction between structural interfaces and base implementation classes.
4. **[Challenge 04 Solution: Getters, Setters, and Static Members](./challenge-04-solution.md)**: Demonstrates property access interception via accessors and class-level memory allocations for shared enterprise utilities.

## Core OOP Design Principles in Practice

### 1. Encapsulation as a Security Boundary
In standard JavaScript, object properties are publicly mutable by default. A junior developer might allow external modules to directly modify object fields (for example, `account.balance = 999999`). In our solutions, we strictly enforce encapsulation:
* **Internal state is hidden**: Sensitive fields are marked `private` or `protected`.
* **State mutation is gated**: External code must interact through public methods or setters that perform rigorous validation, logging, and error handling before touching internal memory.

### 2. Inheritance vs. Composition & Contracts
Our solutions highlight when to use class inheritance (`extends`) versus structural implementation (`implements`):
* **Use `extends`** when child classes share an "is-a" relationship and inherit core behavioral implementations (for example, an `ElectricVehicle` is a specialized `Vehicle`).
* **Use `implements`** when enforcing a behavioral contract across disparate, unrelated class hierarchies (for example, forcing both `Circle` and `Rectangle` to satisfy a `Printable` interface).

### 3. Memory Allocation: Instance vs. Static Members
Understanding memory layout is essential for senior engineers:
* **Instance Members**: Every time `new ClassName()` is executed, fresh memory is allocated on the heap for the object's instance properties (`this.property`).
* **Static Members**: Members marked with `static` are allocated strictly once on the class constructor function object itself. They persist across the entire application lifecycle without requiring object instantiation, making them ideal for registries, singletons, and shared constants.

## Verification & Compile-Time Safety
Every solution file in this directory provides a complete, runnable TypeScript implementation without placeholders or abbreviated code. You can compile and verify these solutions using the TypeScript CLI:

```bash
npx tsc --noEmit
```

Review each detailed solution file to explore symbol-by-symbol tables, common pitfalls, and runtime execution logs.
