# Welcome to Practice Lab: Modules, Path Aliases, and Enterprise Architecture

Welcome to the interactive exercise lab for **Module 08: Modules and Namespaces**! Here is where theoretical knowledge of ES Modules, module resolution, and clean codebase architecture transforms into practical engineering ability.

In enterprise software development, organizing code across thousands of files requires strict boundaries, clean import paths, and build-time optimization. This lab challenges you to solve real-world architectural problems that senior TypeScript engineers face every day.

---

## What You Will Tackle in This Lab

1. **[Challenge 01: Configuring Module Resolution and Path Aliases](./challenge-01.md)**
   - **Core Learning Objective:** Master `tsconfig.json` configuration for `baseUrl` and `paths`.
   - **Engineering Skill:** Eliminate fragile relative paths (`../../../../`) and implement bulletproof absolute path aliases (`@models/*`, `@services/*`, `@utils/*`).

2. **[Challenge 02: Named Exports vs. Default Exports and Renaming](./challenge-02.md)**
   - **Core Learning Objective:** Understand the architectural trade-offs between export styles.
   - **Engineering Skill:** Enforce uniform symbol naming across enterprise codebases using Named Exports, handle legacy integration with Default Exports, and rename symbols on the fly using `as`.

3. **[Challenge 03: Type-Only Imports (`import type`) and Clean Barrel Files (`index.ts`)](./challenge-03.md)**
   - **Core Learning Objective:** Optimize build performance and prevent client-side bundle bloat.
   - **Engineering Skill:** Implement central concierge entrypoints using Barrel Files (`index.ts`), leverage `import type` to strip type blueprints at compile time, and navigate the dangers of barrel file bloat in large monorepos.

---

## How to Work on These Challenges

1. Open each challenge file in numerical order.
2. Read the enterprise scenario, architectural requirements, and specifications carefully.
3. Write your complete TypeScript code and technical explanations directly inside the **ANSWER HERE** section of each challenge file.
4. If you need conceptual clarification, review the core theory and analogies in **[../README.md](../README.md)**.
5. **Remember the Strict Rule:** Do not use em dashes anywhere in your text answers or code comments! Use standard parentheses, colons, or bullet points to structure your thoughts cleanly.

---

## Ready to Check Your Work?

Once you have completed your implementations and technical explanations, compare your work against our verified, production-grade reference solutions inside **[../answers/exercise/](../answers/exercise/)**:
- **[Challenge 01 Solution](../answers/exercise/challenge-01-solution.md)**: Exhaustive path alias configuration and compilation breakdown.
- **[Challenge 02 Solution](../answers/exercise/challenge-02-solution.md)**: Production implementation of named/default exports and refactoring analysis.
- **[Challenge 03 Solution](../answers/exercise/challenge-03-solution.md)**: Optimized type-only import architecture and barrel file design patterns.
- **[Master Exercise Solution Summary](../answers/exercise/exercise-solution.md)**: A complete overview of all three challenge architectures.

Happy coding, and let's build clean, scalable TypeScript architectures!
