# Challenge 02: Generic Constraints with extends

Write generic functions that enforce structural rules on their type arguments using the `extends` keyword.

## Scenario

When you write an unconstrained generic function `<T>`, TypeScript assumes that `T` could be literally anything: a primitive number, a boolean, a string, or an object. Because of this uncertainty, attempting to access specific properties (such as `.name` or `.length`) on an unconstrained type variable results in a compile-time error.

To build robust enterprise utilities, you must use **Generic Constraints** (`T extends Blueprint`). This tells the compiler that you accept any custom type `T`, provided that it possesses at least the minimum required structural properties.

## Your Tasks

1. Implement a constrained generic function `printName<T extends { name: string }>(item: T): void` that logs `item.name` to the console.
2. Implement a generic object merging utility `mergeObjects<T extends object, U extends object>(a: T, b: U): T & U` that combines two objects using the object spread operator (`{ ...a, ...b }`).
3. Verify `printName` with two test cases:
   * Pass an object `{ name: "Alice", age: 30 }`. This should compile cleanly because it satisfies the minimum structural constraint.
   * Attempt to pass an object `{ age: 30 }` (without a `name` property). Write a detailed comment explaining why TypeScript rejects this call at compile time.
4. Verify `mergeObjects` by passing two distinct domain objects (for example, a user identity object and a user permissions object). Log the merged result and document what TypeScript infers as the intersection return type in a comment.

## Architectural Requirements

* Do not use the `any` keyword or type assertions (`as`).
* Ensure that both functions enforce structural constraints via `extends`.
* Do not use em-dashes anywhere in your code or comments.

## ANSWER HERE

```typescript
// Write your printName and mergeObjects implementations and verification tests below:
```
