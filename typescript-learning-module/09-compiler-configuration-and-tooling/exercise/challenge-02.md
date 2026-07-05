# Challenge 02: Building a Production CI/CD Toolchain Pipeline

In modern software engineering, writing clean TypeScript code is only half the battle. You must also establish a robust execution and verification toolchain that maximizes developer velocity during local development while strictly enforcing quality gates in automated CI/CD (Continuous Integration and Continuous Deployment) pipelines.

## The Scenario

You are tasked with designing the development workflow and automated verification pipeline for a mission-critical payment processing microservice. The engineering team requires:
1. **Rapid Local Development**: Developers need to run and test TypeScript files instantly without waiting for physical JavaScript files to be written to disk.
2. **Continuous Background Compiling**: When debugging complex module interactions, developers need the compiler to watch source files and report errors in real time.
3. **Uncompromising CI/CD Quality Gating**: Before any pull request can be merged into the main branch, automated servers must verify type correctness, inspect code smells, and enforce formatting consistency without cluttering the build server with temporary files.
4. **Production Debugging Support**: When runtime errors occur in production Node.js servers, stack traces must point directly to line numbers in original TypeScript source files.

## Your Tasks

1. **The CI/CD Quality Gate Commands**: Write out the exact terminal commands for the three sequential verification checks required in a production CI/CD pipeline (Type Check, Lint Check, and Format Check). Explain why each command is necessary and specifically explain why the `--noEmit` flag is crucial during automated type checking.
2. **Professional `package.json` Scripts**: Write a complete `scripts` object for a `package.json` file that provides standardized npm commands for local development (using `tsx`), watch mode (using `tsc --watch`), production build generation (using `tsc`), and automated CI/CD verification.
3. **Source Map Demonstration Module**: Write a two-file TypeScript module (`src/calculator.ts` and `src/main.ts`) that implements a safe division function. Explain how enabling `"sourceMap": true` in `tsconfig.json` creates `.js.map` files and describe the exact technical mechanism connecting a runtime exception in `dist/main.js` back to `src/main.ts`.

---

## ANSWER HERE

### 1. The CI/CD Quality Gate Commands

* **Step 1 (Type Checking)**: `...`
  * **Why it is necessary**: 
  * **Why `--noEmit` is crucial**: 

* **Step 2 (Linting with ESLint)**: `...`
  * **Why it is necessary**: 

* **Step 3 (Formatting with Prettier)**: `...`
  * **Why it is necessary**: 

### 2. Professional `package.json` Scripts

```json
{
  "scripts": {
    // Write your standardized npm scripts here
  }
}
```

### 3. Source Map Demonstration Module & Explanation

**`src/calculator.ts`**:
```typescript
// Write safe division function with strict type annotations
```

**`src/main.ts`**:
```typescript
// Write entry point importing and executing calculator functions
```

**Technical Explanation of Source Map Mechanics**:
> Write your explanation here detailing how `.js.map` files bridge machine code and human source code during debugging.
