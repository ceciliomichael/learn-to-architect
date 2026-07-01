# Question 02: Structural Typing & Branded Types

During a senior system design interview, you are asked about type compatibility across module boundaries.

Suppose you have two modules in a financial system:
```typescript
// Module A:
type USD = number;
function processPayment(amount: USD): void { /* ... */ }

// Module B:
type EUR = number;
const invoiceTotal: EUR = 100;
```

1. If someone calls `processPayment(invoiceTotal)`, will TypeScript throw a compiler error? Explain why or why not using the concept of **structural typing**.
2. How do **Branded Types** (using intersection with a unique symbol or literal tag) modify TypeScript's structural behavior to simulate **nominal typing**?
3. Write the exact type definitions for `USD` and `EUR` using Branded Types so that passing an `EUR` value into `processPayment` causes a compile-time error.

## ANSWER HERE

> **1. Compiler behavior and why:**

> **2. How Branded Types simulate nominal typing:**

```typescript
// 3. Branded type definitions:

```
