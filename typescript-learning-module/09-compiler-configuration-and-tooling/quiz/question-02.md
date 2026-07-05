# Question 02: The Billion-Dollar Mistake and strictNullChecks

In 1965, computer scientist Tony Hoare invented the null reference while designing the ALGOL W programming language. Decades later, he publicly apologized and named it his **"Billion-Dollar Mistake"** because unhandled null and undefined references have caused countless system crashes, data corruption incidents, and security vulnerabilities across the industry.

## Conceptual Questions

1. Explain exactly how TypeScript treats `null` and `undefined` when `"strictNullChecks": false` is set in `tsconfig.json`. Why does this default setting perpetuate the Billion-Dollar Mistake?
2. When you enable `"strictNullChecks": true`, how does TypeScript's type system change its rules regarding variable assignment and optional properties?
3. Provide a concrete code example demonstrating a function that would compile cleanly under `"strictNullChecks": false` but crash at runtime. Then, show how `"strictNullChecks": true` catches the bug at compile time and how a developer must use **Type Narrowing** to resolve the compiler error safely.

---

## ANSWER HERE

> **1. Behavior under `"strictNullChecks": false`:**

> **2. Transformation under `"strictNullChecks": true`:**

> **3. Concrete Code Example and Type Narrowing Fix:**
```typescript
// Write your code example and explanation here
```
