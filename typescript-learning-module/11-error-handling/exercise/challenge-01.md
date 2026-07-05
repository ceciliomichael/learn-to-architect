# Challenge 01: try / catch / finally in Practice

In TypeScript strict mode, all caught exceptions in a `catch` block are typed as `unknown` by default. This forces you to verify the runtime type of the error before accessing properties like `.message` or `.stack`. Furthermore, when working across input/output boundaries (like parsing external JSON payloads or accessing database resources), you need guaranteed cleanup mechanics using the `finally` block.

## Your Tasks

1. Write a synchronous function `parseJSON(input: string): object` that:
   - Uses `JSON.parse(input)` inside a `try` block and casts or types the return value cleanly as an `object`.
   - Catches any error thrown by `JSON.parse` (in JavaScript, invalid JSON triggers a native `SyntaxError`).
   - Narrows the caught error using `instanceof Error`. If it is an `Error` object, rethrow a new descriptive error: `throw new Error("Invalid JSON: " + error.message)`. If it is not an `Error` object, throw `new Error("Invalid JSON: Unknown error occurred.")`.
   - Has a `finally` block that logs `"Parse attempt finished."` to the console, demonstrating unconditional execution.

2. Write an asynchronous function `safeParseJSON(input: string): Promise<object | null>` that:
   - Calls `parseJSON(input)` inside a `try` block and returns the parsed object upon success.
   - On error, catches the exception, checks if it is `instanceof Error`, logs `"Caught: " + error.message` to the console, and safely returns `null` instead of crashing the application.

3. Test your implementation with two test calls:
   - One call passing a valid JSON string: `'{"name": "Alice", "age": 30}'`.
   - One call passing an invalid JSON string: `"this is not valid json"`.

## ANSWER HERE

```typescript
// Write parseJSON and safeParseJSON implementations and test calls here
```
