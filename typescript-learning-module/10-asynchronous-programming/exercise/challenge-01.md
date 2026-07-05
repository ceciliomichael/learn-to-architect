# Challenge 01: Write Your First Async Function

Practice creating Promises and using async/await.

## Your Tasks

1. Write an async function `simulateDelay(ms: number): Promise<string>` that
   - Wraps a `setTimeout` inside `new Promise`.
   - After `ms` milliseconds, resolves with the string `"Done after " + ms + "ms"`.

2. Write an `async function main(): Promise<void>` that
   - Awaits `simulateDelay(500)` and logs the result.
   - Then awaits `simulateDelay(200)` and logs that result too.

3. Call `main()` at the bottom of the file.

4. In comments, note the difference between calling `main()` and calling `await main()` at the top level.

## ANSWER HERE

```typescript
// Write simulateDelay and main here
```
