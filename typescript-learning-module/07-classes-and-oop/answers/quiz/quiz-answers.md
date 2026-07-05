# Module 07 Quiz Answers: Architectural Overview

This document serves as the master architectural reference and explanation index for all conceptual quiz questions in Module 07 (Classes and Object-Oriented Programming). 

In technical interviews and production code reviews, understanding *how* the TypeScript compiler transforms Object-Oriented syntax into runtime JavaScript is essential for preventing security leaks, memory bloat, and architectural anti-patterns. Below is the index of detailed conceptual answers and deep-dive explanations.

## Quiz Answer Index & Deep-Dive Guides

1. **[Question 01 Answer: Access Modifiers at Runtime](./question-01-answer.md)**: Explains compile-time erasure of `private`/`protected`, runtime JavaScript object inspection, and true ECMAScript private fields (`#field`).
2. **[Question 02 Answer: private vs protected](./question-02-answer.md)**: Deconstructs inheritance boundaries, subclass access rights, and enterprise use cases for protected base class members.
3. **[Question 03 Answer: Parameter Property Shorthand](./question-03-answer.md)**: Explains compiler syntax desugaring, constructor boilerplate reduction, and rules for computed property initialization.
4. **[Question 04 Answer: `extends` vs `implements`](./question-04-answer.md)**: Contrasts class inheritance with structural interface contracts, explaining single inheritance limits versus multiple interface adoption.
5. **[Question 05 Answer: Abstract Classes](./question-05-answer.md)**: Explains base blueprints, uninstantiable class mechanics, and forced subclass method implementation.
6. **[Question 06 Answer: Getters, Setters, and Static Members](./question-06-answer.md)**: Explains property access interception via accessors and memory allocation of static members on class constructor objects.

## Summary of Critical Conceptual Takeaways

### 1. Compile-Time Erasure vs. Runtime Reality
Never rely on TypeScript's `private` or `protected` keywords for cryptographic privacy or runtime data security! TypeScript types and access modifiers are completely erased during compilation to standard JavaScript. When executed in Node.js or a web browser, a `private` TypeScript property is a plain, publicly accessible JavaScript object property. For unbreakable runtime privacy, use ECMAScript hash-prefixed private fields (`#secretKey`), which are enforced directly by the JavaScript V8/SpiderMonkey runtime engine.

### 2. Single Inheritance vs. Multiple Interfaces
TypeScript and JavaScript strictly enforce **Single Inheritance**: a class can only extend exactly one parent class (`class Child extends Parent`). This prevents the infamous "Diamond Problem" where a class inherits conflicting method implementations from multiple parents. However, a class can implement **Multiple Interfaces** (`class Report implements Printable, Serializable, Loggable`) because interfaces contain zero implementation logic; they are purely structural contracts that check method signatures during compilation.

### 3. Memory Footprint of Static Utilities
When designing shared enterprise utilities (such as loggers, configuration loaders, or database connection pool managers), attach methods and constants to the class using the `static` keyword. Static members reside strictly on the class constructor function object in memory. This avoids allocating redundant prototype chains and object instances on the heap whenever a utility method is invoked across different modules.
