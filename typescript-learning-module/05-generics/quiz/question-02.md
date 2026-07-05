# Question 02: Generic Constraints

Examine how the `extends` keyword enforces structural contracts on generic type variables to prevent compile-time property lookup errors.

## Code Scenario

Consider the following generic utility function designed to measure the length of an incoming item:

```typescript
function getLength<T>(item: T): number {
  return item.length; // TypeScript throws a compile-time error here!
}
```

## Conceptual Questions

1. Why does the TypeScript compiler throw an error on `item.length` when `T` is declared without a constraint?
2. How do you resolve this compile-time error using the generic constraint keyword `extends`? Write out the corrected function signature.
3. After applying your generic constraint, list at least three distinct data types that TypeScript will accept as valid arguments, and list at least two data types that TypeScript will reject. Explain why structural subtyping (duck typing) makes this constraint so versatile.

## ANSWER HERE

> **1. Why TypeScript throws an error on `item.length`:**

> **2. The corrected function signature using `extends`:**
```typescript
// Write the corrected function below:
```

> **3. Accepted types, rejected types, and structural subtyping analysis:**
