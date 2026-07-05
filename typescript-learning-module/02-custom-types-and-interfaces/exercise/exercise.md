# Welcome to Module 02 Practice Lab: Custom Types & Interfaces

Welcome back! In Module 01, you worked with simple primitives like numbers and strings. But in real software development, we deal with complex data entities: user profiles, game characters, shopping carts, and configuration dictionaries.

In this practice lab, you will act as a software architect modeling real-world data blueprints using **Interfaces** and **Type Aliases**.

---

## What You Will Tackle in This Lab

1. **[Challenge 01: Design a Game Character Blueprint](./challenge-01.md)**: Create a robust interface for a video game RPG character with `readonly` IDs, optional guild affiliations, and skill arrays.
2. **[Challenge 02: Extend Blueprints Two Ways](./challenge-02.md)**: Practice code reuse by inheriting animal properties into bird structures using both interface `extends` and type intersection `&` operators.
3. **[Challenge 03: Translation Dictionary with Index Signatures](./challenge-03.md)**: Build dynamic lookup tables where keys aren't known ahead of time using strict index signatures.
4. **[Challenge 04: Union Types in Action](./challenge-04.md)**: Create flexible ID identifiers that accept strings or numbers, then safely branch logic using `typeof` guards.

---

## How to Work on These Challenges

1. Open your target challenge file.
2. Read the architectural requirements carefully.
3. Write your custom interfaces, types, and test objects directly inside the **`ANSWER HERE`** section.
4. Experiment by intentionally breaking a type rule (like modifying a `readonly` field) just to see what error message TypeScript produces.

---

## Need Assistance?

If you feel stuck on when to choose `type` versus `interface`, review the guidance in **[`../README.md`](../README.md)**. When ready, compare your code against our production implementations in **[`../answers/exercise/`](../answers/exercise/)**. Happy coding!
