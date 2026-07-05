# Question 01: ES Modules vs. Script Mode and Scope Isolation

In TypeScript and modern JavaScript, understanding the boundary between global script execution and modular scope isolation is fundamental to preventing variable collision bugs in large systems.

Consider the following two TypeScript files in an enterprise codebase:

```typescript
// ============================================================================
// FILE: src/legacy/globalLogger.ts (No top-level imports or exports)
// ============================================================================
const appVersion: string = "1.0.0";
const maxRetryCount: number = 3;

function initializeSystem(): void {
  console.log(`System starting at version ${appVersion}`);
}
```

```typescript
// ============================================================================
// FILE: src/services/authService.ts (Contains an import statement)
// ============================================================================
import { DatabaseConnection } from "../database/connection";

const appVersion: string = "2.5.0";
const maxRetryCount: number = 5;

export class AuthService {
  public authenticate(): boolean {
    return true;
  }
}
```

## Your Challenge

Answer the following four architectural questions directly inside the **ANSWER HERE** block below. Do not use em dashes anywhere in your response!

1. In `src/legacy/globalLogger.ts`, are `appVersion` and `maxRetryCount` scoped strictly to that file, or are they added to the global execution scope across the entire application? Explain the exact rule TypeScript uses to determine this behavior.
2. In `src/services/authService.ts`, are `appVersion` and `maxRetryCount` scoped to that file or global? Why does the presence of an `import` statement alter how the TypeScript compiler treats the file's variables?
3. What happens during compilation if both `src/legacy/globalLogger.ts` and another script file (such as `src/legacy/metrics.ts` lacking imports/exports) both declare `const appVersion: string = "1.0.0"`? What exact compiler error or runtime behavior occurs?
4. What is the cleanest, standard TypeScript syntax you can add to `src/legacy/globalLogger.ts` to convert it into an isolated ES Module without actually exporting or importing any runtime symbols?

---

## ANSWER HERE

### 1. Scope behavior of `src/legacy/globalLogger.ts`:
> 

### 2. Scope behavior of `src/services/authService.ts`:
> 

### 3. Consequence of duplicate declarations across script files:
> 

### 4. Syntax to force module isolation without runtime imports/exports:
> 
