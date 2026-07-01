# Answer  -  Question 02: Structural Typing & Branded Types

## 1. Compiler Behavior & Why
TypeScript **will not throw a compiler error**. Because `type USD = number;` and `type EUR = number;` are pure type aliases, TypeScript uses **structural typing**. Both types structurally resolve to primitive `number`. To the compiler, passing an `EUR` variable into a function expecting `USD` is simply passing a `number` where a `number` is expected.

## 2. How Branded Types Simulate Nominal Typing
To simulate nominal typing, we intersect the primitive type with an object shape containing a unique string tag or `unique symbol` property: `number & { readonly __brand: "USD" }`. Because an `EUR` branded type has `{ readonly __brand: "EUR" }`, their structural shapes diverge completely! TypeScript rejects assigning one to the other, even though at runtime both are just plain numbers (the brand object never exists in runtime memory).

## 3. Branded Type Definitions

```typescript
export type Brand<K, T> = K & { readonly __brand: T };

export type USD = Brand<number, "USD">;
export type EUR = Brand<number, "EUR">;

export function createUSD(amount: number): USD {
  if (amount < 0) throw new Error("Amount cannot be negative.");
  return amount as USD;
}

export function createEUR(amount: number): EUR {
  if (amount < 0) throw new Error("Amount cannot be negative.");
  return amount as EUR;
}

function processPayment(amount: USD): void {
  console.log(`Processing $${amount}`);
}

const invoiceTotal = createEUR(100);

// COMPILE ERROR: Argument of type 'Brand<number, "EUR">' is not assignable to parameter of type 'Brand<number, "USD">'.
// processPayment(invoiceTotal);
```
