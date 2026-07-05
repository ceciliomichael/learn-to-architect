# Welcome to Conceptual Quiz: Error Handling

Welcome to the conceptual quiz for **Error Handling**! True engineering mastery requires understanding *why* language mechanics operate under the hood, not just memorizing syntax rules.

These questions are structured to test your architectural mental models, prototype chain understanding, and compiler awareness. Mastering these concepts will prepare you for rigorous technical interviews and system design reviews.

## Topics We Are Testing Today

1. **[Question 01: unknown in catch](./question-01.md)** - Explore why strict mode enforces `unknown` instead of `Error` in exception handlers, and how to narrow unknown objects safely.
2. **[Question 02: When Does finally Run?](./question-02.md)** - Analyze call stack unwinding, return statement interception, and resource cleanup guarantees in `finally` blocks.
3. **[Question 03: Custom Error Classes & Prototype Mechanics](./question-03.md)** - Examine the trade-offs between generic error strings and custom hierarchies, `instanceof` narrowing, `this.name`, and prototype chain restoration (`Object.setPrototypeOf`).

## How to Take This Quiz

1. Open each question file sequentially in your workspace.
2. Think through the compiler and runtime mechanics before peeking at any notes or answers.
3. Write your architectural reasoning clearly inside the **ANSWER HERE** block.

## Check Your Answers

When you have completed your responses, verify your understanding against our exhaustive, production-grade explanations inside **[../answers/quiz/](../answers/quiz/)**. Let's see how well you know TypeScript error boundaries!
