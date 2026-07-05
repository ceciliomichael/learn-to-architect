# Question 01 Answer: ES Modules vs. Script Mode and Scope Isolation

This document provides the exhaustive, deeply technical reference answer for Question 01, detailing the architectural boundaries between global script execution and ES Module scope isolation in TypeScript.

---

### 1. Scope Behavior of `src/legacy/globalLogger.ts`
In `src/legacy/globalLogger.ts`, the variables `appVersion` and `maxRetryCount` are **added directly to the global execution scope across the entire application**. 

**The Exact TypeScript Compiler Rule**: By definition according to the ECMAScript specification and TypeScript compiler rules, any file that **lacks top-level `import` or `export` statements** is treated as a traditional **Script** rather than a Module. In script mode, all top-level variable declarations (`var`, `let`, `const`), function declarations, and class declarations are merged into the global namespace (such as `window` in browsers or `global` in Node.js). As a result, these symbols are accessible without importation by every other script file in the project, creating severe risk of variable shadowing and naming collisions.

---

### 2. Scope Behavior of `src/services/authService.ts`
In `src/services/authService.ts`, the variables `appVersion` and `maxRetryCount` are **strictly file-scoped (private to that module)**.

**Why an `import` Statement Alters Compiler Behavior**: The moment the TypeScript compiler observes at least one top-level `import` or `export` statement inside a file, it automatically transitions its classification of that file from a Script to an **ES Module**. In an ES Module, every top-level declaration is strictly encapsulated within that file's module lexical scope. No symbols can leak out into the global namespace or be accessed by external files unless they are explicitly marked with the `export` keyword.

---

### 3. Consequence of Duplicate Declarations Across Script Files
If both `src/legacy/globalLogger.ts` and another script file (such as `src/legacy/metrics.ts`) declare `const appVersion: string = "1.0.0"`, **the TypeScript compiler immediately throws a fatal compile-time error across both files**:
```text
Error: Cannot redeclare block-scoped variable 'appVersion'.
```
**Why This Occurs**: Because neither file contains an `import` or `export` statement, TypeScript treats both files as contributing to the exact same global scope container. Since variables declared with `const` or `let` cannot be redeclared within the same lexical scope in JavaScript, declaring `appVersion` twice in the global scope causes an immediate redeclaration collision. In a large enterprise team, this behavior makes global scripts untenable for production engineering.

---

### 4. Syntax to Force Module Isolation Without Runtime Imports/Exports
The cleanest, universally accepted architectural pattern to convert a global script file into an isolated ES Module without importing or exporting any runtime symbols is adding an empty export statement:
```typescript
// Adding an empty export statement converts the script into an isolated ES Module:
export {};

const appVersion: string = "1.0.0";
const maxRetryCount: number = 3;
```
**How This Works**: The syntax `export {};` explicitly instructs the TypeScript compiler that this file is an ES Module exporting zero named symbols. Because an `export` statement is present, TypeScript encapsulates `appVersion` and `maxRetryCount` within the file's private module scope, immediately eliminating global scope pollution and preventing variable collision errors.
