# Question 02 Answer

**No, TypeScript does not throw an error on the `.push()` line.**

`const` protects the **variable binding**  -  it prevents you from reassigning the variable to point at a completely different value. It does not protect the internal contents of whatever the variable points to.

When you write `const scores = [90, 85]`, the variable `scores` is locked to that specific array object in memory. You cannot do `scores = [1, 2, 3]` (that would reassign the variable). But the array object itself is not frozen. You can still add items, remove items, or change items within it because those operations modify the array, not the variable.

`.push()` modifies the existing array. It does not replace it. So `const` has no objection.

If you want to prevent all mutation, use `as const` which makes the array and its contents fully readonly
```typescript
const scores = [90, 85] as const;
scores.push(100); // ERROR! Cannot mutate a readonly array.
```
