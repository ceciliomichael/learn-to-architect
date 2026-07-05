# Question 04: Execution Toolchains and CI/CD Quality Gating

Professional software engineering requires choosing the right tools for different stages of the development lifecycle. What works best for rapid local prototyping is rarely appropriate for automated production verification on Continuous Integration (CI/CD) servers.

## Conceptual Questions

1. Why is the traditional workflow of running `tsc` followed by `node dist/index.js` considered anti-pattern for local development? How do direct execution engines like **`tsx`** (powered by Esbuild) or **`ts-node`** solve this bottleneck?
2. When configuring automated verification pipelines on CI/CD servers (such as GitHub Actions or AWS CodePipeline), why is it critical to run `tsc --noEmit` instead of a standard `tsc` build command during the pull request verification stage? What resources does `--noEmit` conserve?
3. Explain the distinct architectural roles of **TypeScript (`tsc`)**, **ESLint**, and **Prettier** in the frontend and backend engineering ecosystem. Why is TypeScript alone insufficient to guarantee codebase quality and maintainability?

---

## ANSWER HERE

> **1. Local Development Bottlenecks vs. In-Memory Execution Engines (`tsx`):**

> **2. The Strategic Role of `--noEmit` in CI/CD Pipelines:**

> **3. The Holy Trinity: Distinct Roles of `tsc`, ESLint, and Prettier:**
