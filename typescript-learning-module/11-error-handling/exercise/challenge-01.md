# Challenge 01: try/catch/finally in Practice

Practice the full error handling structure on a real scenario.

## Your Tasks

1. Write a function `parseJSON(input: string): object` that:
   - Uses `JSON.parse(input)` inside a `try` block.
   - Catches any error thrown by `JSON.parse` (it throws a `SyntaxError` for invalid JSON).
   - Rethrows it as a `new Error("Invalid JSON: " + the original message)`.
   - Has a `finally` block that logs `"Parse attempt finished."`.

2. Write an async function `safeParseJSON(input: string): Promise<object | null>` that:
   - Calls `parseJSON(input)` inside a `try` block.
   - Returns the parsed object on success.
   - On error, logs `"Caught: " + error.message` (check `instanceof Error`) and returns `null`.

3. Test with two calls: one valid JSON string and one invalid string.

## ANSWER HERE

```typescript
// Write parseJSON and safeParseJSON here:


```
