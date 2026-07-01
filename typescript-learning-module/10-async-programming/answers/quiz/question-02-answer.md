# Question 02 Answer

**Type of `data` and what `console.log(data)` shows:**
The type of `data` is `Promise<{ name: string }>`  -  a Promise object, not the resolved value. `console.log(data)` immediately shows something like `Promise { <pending> }` because the Promise has not resolved yet. The actual `{ name: "Alice" }` value is locked inside the Promise until you await it.

**Error on `data.name`:**
TypeScript produces a compile error:
```
Property 'name' does not exist on type 'Promise<{ name: string }>'.
```
You are trying to access `.name` on the Promise wrapper, not on the resolved value inside it. TypeScript correctly blocks this.

**The fix:**
`await`:
```typescript
const data = await fetchUserData(); // Now data is { name: string }
console.log(data.name);            // "Alice"  -  works correctly.
```
