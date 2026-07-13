# Welcome to Senior Architectural Practice Lab
Welcome to the systems design and architectural coding lab! This lab goes beyond syntax to test your ability to build production-grade, compile-time safe systems.

In real tech company interviews (Google, Meta, Stripe), senior engineering candidates are asked to demonstrate deep understanding of type mechanics, structural invariants, and state management.

---

## What You Will Tackle in This Lab

1. **[Challenge 01: The Branded ID Architecture](./challenge-01.md)** - Prevent accidental mixing of user and order identifiers with zero-runtime-overhead branded types.
2. **[Challenge 02: Discriminated Union State Machine & Exhaustiveness Guard](./challenge-02.md)** - Model request states and prove every state is handled with a `never` exhaustiveness guard.
3. **[Challenge 03: Async Resilience & The Result Pattern](./challenge-03.md)** - Convert asynchronous failures into an explicit `Result<T, E>` contract.

---

## How to Work on These Challenges

1. Open each challenge file sequentially.
2. Read the architectural constraints and requirements.
3. Write your implementation inside the **`ANSWER HERE`** section.
4. Test edge cases mentally or in a scratch file to ensure type safety cannot be bypassed.

---

## Verify Your Solutions

Once you have completed your implementations, compare your code against our exhaustive senior engineering solutions inside **[`../answers/exercise/`](../answers/exercise/)**. Great job pushing your skills to the next level!

