# Module 02 Exercise Solutions: Master Reference

This document provides exhaustive, production-grade reference solutions for all four challenges in Module 02. Each solution includes complete TypeScript code, architectural trade-offs, memory/runtime implications, and symbol-by-symbol breakdowns.

---

## Challenge Overview & Quick Navigation

1. **[Challenge 01 Solution: Game Character Blueprint](./challenge-01-solution.md)**: Modeling domain entities with `readonly` modifiers, optional properties (`?`), and arrays.
2. **[Challenge 02 Solution: Extend Blueprints Two Ways](./challenge-02-solution.md)**: Comparing interface inheritance (`extends`) against type alias intersection (`&`).
3. **[Challenge 03 Solution: Translation Dictionary](./challenge-03-solution.md)**: Mastering dynamic lookup tables with strict index signatures (`[key: string]: string`).
4. **[Challenge 04 Solution: Union Types in Action](./challenge-04-solution.md)**: Designing flexible identifier types (`string | number`) and runtime narrowing using `typeof` type guards.

---

## Architectural Philosophy: Why These Patterns Matter

In production TypeScript engineering, designing data blueprints is not merely about making the compiler happy; it is about establishing clear structural boundaries and domain contracts across distributed teams:

### 1. Immutability at the Boundary (`readonly`)
In enterprise databases (such as PostgreSQL or MongoDB), primary keys like UUIDs or auto-incrementing integers must remain invariant throughout an entity's lifecycle. Marking identifiers as `readonly id: string` at the TypeScript interface level guarantees that domain logic cannot inadvertently reassign or mutate unique database keys in memory.

### 2. Expressing Domain Flexibility (`?` vs `| undefined`)
Real-world data is inherently messy. Users omit optional profile fields, third-party APIs return partial payloads, and configuration files rely on fallback defaults. Using optional property modifiers (`property?: string`) allows architectures to model optionality cleanly without forcing consumers to explicitly boilerplate `undefined` checks during object instantiation.

### 3. Scalable Composition (`extends` vs `&`)
When building extensible domain models or design systems, duplication is the root cause of divergence. Whether utilizing interface inheritance (`extends`) or type intersections (`&`), composing smaller, single-responsibility shapes into complex aggregates ensures DRY (Don't Repeat Yourself) domain models and predictable refactoring.

---

## How to Use These Solution Guides

Do not simply copy and paste the code into your lab. For each challenge solution:
1. Examine the **Complete TypeScript Implementation** and compare your syntax against the production standard.
2. Read the **Symbol-by-Symbol Breakdown** to ensure you understand the exact grammatical role of every punctuation mark and keyword.
3. Study the **Architectural Trade-offs & Runtime Implications** to understand why senior engineers make specific design decisions when building scalable software systems.
