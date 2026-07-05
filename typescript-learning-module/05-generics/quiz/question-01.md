# Question 01: any vs. Generics

Examine the fundamental difference between disabling TypeScript's static type checker using `any` versus preserving type identity using Generics `<T>`.

## Code Scenario

Consider the following two functions that both accept an argument and return it unmodified:

```typescript
function processAny(arg: any): any {
  return arg;
}

function processSafe<T>(arg: T): T {
  return arg;
}
```

## Conceptual Questions

1. Suppose a developer executes `const result1 = processAny("hello")`. What does TypeScript infer as the type of `result1`? What happens at compile time and at runtime if the developer subsequently executes `result1.toFixed(2)`?
2. Suppose a developer executes `const result2 = processSafe("hello")`. What does TypeScript infer as the type of `result2`? What happens at compile time if the developer subsequently executes `result2.toFixed(2)`?
3. In your own words, explain what a generic type variable (`<T>`) actually represents in compiler memory, and why it is architecturally superior to using `any` for polymorphic utilities.

## ANSWER HERE

> **1. Type of `result1` and behavior of `.toFixed(2)`:**

> **2. Type of `result2` and behavior of `.toFixed(2)`:**

> **3. Architectural meaning and superiority of `<T>`:**
