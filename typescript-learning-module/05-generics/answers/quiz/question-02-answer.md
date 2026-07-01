# Question 02 Answer

**Why TypeScript errors on `item.length`:**
Without a constraint, `T` can be absolutely any type  -  a number, a boolean, a function, anything. Most types do not have a `length` property. TypeScript does not know whether `T` has `length`, so it blocks the access to be safe.

**The fix using extends:**

```typescript
function getLength<T extends { length: number }>(item: T): number {
  return item.length;
}
```

The constraint `<T extends { length: number }>` tells TypeScript: "`T` can be any type, but only if it has a `length` property that is a number." Now TypeScript can guarantee `item.length` exists.

**What types are now accepted:**
- Strings (`"hello"` has `.length`)
- Arrays (`[1, 2, 3]` has `.length`)
- Any object with a numeric `length` property

**What types are still rejected:**
- Numbers (`42` has no `.length`)
- Booleans (`true` has no `.length`)
- Plain objects without a `length` property (`{ name: "Alice" }`)
