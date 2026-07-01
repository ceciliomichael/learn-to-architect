# Module 05 Exercise: Generics & Constraints

Complete your solutions inside the **ANSWER HERE** code blocks below.

---

### Challenge 1: Generic Array First Element
Write a generic function called `getFirstElement<T>` that accepts an array of type `T[]`.
1. If the array is empty (`arr.length === 0`), return `undefined`.
2. Otherwise, return the first element (`arr[0]`).
3. Ensure the return type is strictly typed as `T | undefined`. Test calling it with both a `string[]` and a `number[]`.

#### ✍️ ANSWER HERE:
```typescript
// Write your getFirstElement function and tests here:


```

---

### Challenge 2: Generic Constraints (`extends`)
Write a generic function called `mergeNamedObjects<T extends { name: string }, U extends { name: string }>(obj1: T, obj2: U)` that returns a combined object containing properties from both objects.
If you try to pass `{ age: 25 }` (an object without `name`) as `obj1`, TypeScript should throw a compiler error!

#### ✍️ ANSWER HERE:
```typescript
// Write your mergeNamedObjects function here:


```

---

### Challenge 3: Generic Interfaces with Default Types
Create a generic interface `PaginatedResponse<T = string>`:
1. `data`: An array of `T` (`T[]`).
2. `currentPage`: number.
3. `totalPages`: number.

Create two objects using this interface: one where you let `<T>` default to `string`, and another where you explicitly pass `<{ id: number; username: string }>` as `T`.

#### ✍️ ANSWER HERE:
```typescript
// Write your PaginatedResponse interface and objects here:


```
