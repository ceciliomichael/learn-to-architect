# Welcome to Conceptual Quiz: Modules, Path Aliases, and Enterprise Architecture

Welcome to the conceptual quiz for **Module 08: Modules and Namespaces**! True engineering mastery requires understanding *why* code works under the hood, how the TypeScript compiler evaluates module boundaries, and how runtime JavaScript engines execute ES Modules.

These five questions are designed to test your architectural mental models and prepare you for real-world enterprise code reviews, system design discussions, and technical interviews.

---

## Topics We Are Testing Today

1. **[Question 01: ES Modules vs. Script Mode and Scope Isolation](./question-01.md)**
   - Test your understanding of global script pollution versus module scope isolation, and explain how top-level import/export statements alter compiler behavior.

2. **[Question 02: Named vs. Default Exports and Enterprise Refactoring Safety](./question-02.md)**
   - Analyze the architectural trade-offs between export styles, import renaming syntax (`as`), and why enterprise engineering teams universally favor named exports for refactoring safety.

3. **[Question 03: Type-Only Imports (`import type`) and Build Bundle Optimization](./question-03.md)**
   - Examine how build bundlers process type imports, how `import type` prevents server-side code bloat in client bundles, and how inline type imports function in modern TypeScript.

4. **[Question 04: Barrel Files (`index.ts`) and Monorepo Performance Traps](./question-04.md)**
   - Explore the concierge desk pattern for re-exporting modules, and evaluate the severe performance risks of barrel file bloat and circular dependencies in large monorepos.

5. **[Question 05: Module Resolution, Path Aliases (`@/*`), and Node.js ESM `.js` Extension](./question-05.md)**
   - Deep dive into `baseUrl` and `paths` compiler resolution, the critical difference between compile-time path aliases and runtime Node.js execution, and why native Node.js ES Modules require explicit `.js` extensions.

---

## How to Take This Quiz

1. Open each question file sequentially in numerical order.
2. Think through the compiler mechanics, AST evaluation, and runtime behavior before consulting reference materials.
3. Write your reasoning clearly inside the **ANSWER HERE** block of each question file.
4. **Remember the Strict Rule:** Do not use em dashes anywhere in your text answers or code comments! Use standard parentheses, colons, or bullet points to structure your explanations.

---

## Check Your Answers

When you have completed your conceptual responses, verify your answers against our exhaustive, production-grade architectural explanations inside **[../answers/quiz/](../answers/quiz/)**:
- **[Question 01 Answer](../answers/quiz/question-01-answer.md)**: Comprehensive breakdown of script mode vs. ES Module scope isolation.
- **[Question 02 Answer](../answers/quiz/question-02-answer.md)**: Enterprise analysis of named vs. default exports and refactoring AST mechanics.
- **[Question 03 Answer](../answers/quiz/question-03-answer.md)**: Deep dive into `import type` compilation erasure and bundle tree-shaking.
- **[Question 04 Answer](../answers/quiz/question-04-answer.md)**: Exhaustive analysis of barrel files, monorepo bloat, and circular dependency prevention.
- **[Question 05 Answer](../answers/quiz/question-05-answer.md)**: Step-by-step module resolution algorithm and Node.js ESM runtime rules.
- **[Master Quiz Answer Summary](../answers/quiz/quiz-answers.md)**: A unified master reference document covering all five conceptual solutions.

Let's see how many you ace!
