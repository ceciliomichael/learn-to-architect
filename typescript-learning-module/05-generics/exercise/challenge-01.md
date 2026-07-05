# Challenge 01: Generic Safe Getter

Write a universal function that works with any array type while maintaining 100% compile-time type safety and preventing runtime crashes from undefined array indexing.

## Scenario

In enterprise software development, accessing array elements by index (such as `arr[0]`) is a frequent source of runtime exceptions when arrays are empty. If a developer writes a helper function using `any` to accept arbitrary arrays, TypeScript loses all ability to track the data type of the returned element.

Your goal is to build a type-safe generic getter that captures the incoming array element type and guarantees that the caller receives either the exact item type or `undefined`.

## Your Tasks

1. Implement a generic function `getFirstElement<T>(arr: T[]): T | undefined` that adheres to these rules:
   * Returns `arr[0]` if the array contains at least one element.
   * Returns `undefined` if the array is empty.
2. Test your function with three distinct call sites:
   * A `string[]` (for example, `["apple", "banana", "cherry"]`). Log the result and write a comment indicating what TypeScript infers as the return type.
   * A `number[]` (for example, `[95, 82, 100]`). Log the result and write a comment indicating what TypeScript infers as the return type.
   * An empty array `[]`. For this call, explicitly specify the type parameter as `getFirstElement<string>([])`. Log the result and explain in a comment why explicit parameter passing is necessary for empty array literals.

## Architectural Requirements

* Do not use the `any` keyword or type assertions (`as`).
* Ensure that your code compiles cleanly under TypeScript's `strict` mode.
* Do not use em-dashes anywhere in your code or comments.

## ANSWER HERE

```typescript
// Write your getFirstElement implementation and verification tests below:
```
