# Challenge 02: Generic Constraint with extends

Write a generic function that requires its type argument to have a specific property.

## Your Tasks

1. Write a function `printName<T extends { name: string }>(item: T): void` that logs `item.name`.

2. Write a function `mergeObjects<T extends object, U extends object>(a: T, b: U): T & U` that merges two objects together. Hint: you can use `{ ...a, ...b }` to merge objects (the spread operator copies all properties from each object into a new one).

3. Test `printName` with:
   - An object `{ name: "Alice", age: 30 }`  -  should work.
   - An object `{ age: 30 }` (no name)  -  write the TypeScript error in a comment.

4. Test `mergeObjects` with two different objects and log the result. Note what TypeScript infers as the return type in a comment.

## ANSWER HERE

```typescript
// Write printName and mergeObjects here:


```
