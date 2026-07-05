# Question 02: Named vs. Default Exports and Enterprise Refactoring Safety

When architecting shared libraries across teams, choosing between **Named Exports** and **Default Exports** has profound implications for code maintainability, searchability, and automated tool support.

Consider the following utility module:

```typescript
// ============================================================================
// FILE: src/utils/mathUtilities.ts
// ============================================================================
export const PI: number = 3.14159;
export const TAX_RATE: number = 0.15;

export function calculateCircleArea(radius: number): number {
  return PI * radius * radius;
}

export default class EnterpriseFinancialEngine {
  public computeTotalWithTax(amount: number): number {
    return amount + amount * TAX_RATE;
  }
}
```

## Your Challenge

Answer the following four architectural questions directly inside the **ANSWER HERE** block below. Do not use em dashes anywhere in your response!

1. Write the exact TypeScript import statement required in `src/main.ts` to import `PI`, `calculateCircleArea`, and `EnterpriseFinancialEngine` in a single line of code.
2. Show the exact syntax for renaming the named import `calculateCircleArea` to `computeArea` on the fly. How does renaming a default import differ from renaming a named import?
3. Why do senior engineering teams and enterprise style guides (such as Google and Microsoft) universally prefer **Named Exports** over **Default Exports** across large monorepos? Provide at least two concrete engineering justifications.
4. Explain how **Default Exports** impair automated IDE refactoring tools (such as "Rename Symbol across Workspace") and codebase symbol searching. What goes wrong when three different teams import `EnterpriseFinancialEngine` into their services under three different random local names?

---

## ANSWER HERE

### 1. Combined import statement:
```typescript
// Write your import statement here:
```

### 2. Renaming syntax and comparison:
> **Renaming named import syntax:**
> 

> **How renaming default imports differs:**
> 

### 3. Engineering justifications for preferring Named Exports:
> 

### 4. Impact of Default Exports on IDE refactoring and symbol searching:
> 
