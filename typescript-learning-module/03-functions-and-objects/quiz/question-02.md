# Question 02: void Callbacks

You define a function that accepts a callback
```typescript
function runOnce(cb: () => void): void {
  cb();
}
```

You then call it like this
```typescript
runOnce(() => true);
```

The callback `() => true` returns a `boolean`, but the callback type is `() => void`.

1. Does TypeScript throw an error here? Why or why not?
2. What does `void` mean as a callback return type? Does it mean the callback must return nothing, or something else?
3. Why was TypeScript designed to allow this?

## ANSWER HERE

> **Does it error?** No. TypeScript allows a value-returning function where a context expects a `void`-returning callback.

> **What void means in a callback return type:** The caller promises to ignore the callback's return value. The callback still returns `true` at runtime, but `runOnce` cannot use that value through its `() => void` contract.

> **Why TypeScript was designed this way:** This supports common JavaScript patterns in which callbacks return incidental values that the receiving API ignores, such as passing `item => destination.push(item)` to `.forEach()`.
