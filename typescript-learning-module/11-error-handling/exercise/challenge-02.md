# Challenge 02: Custom Error Classes

Throwing generic `new Error("some message")` objects makes programmatic error handling difficult in complex enterprise applications. By building custom domain error classes that inherit from `Error`, you allow calling code to use `instanceof` to branch logically based on the exact failure type.

In TypeScript, when extending native classes like `Error`, you must explicitly restore the prototype chain inside the constructor using `Object.setPrototypeOf(this, new.target.prototype)`. Without this essential syntax, `instanceof` checks may fail in transpiled ES5 environments!

## Your Tasks

1. Create a custom error class `ValidationError extends Error`:
   - Include a public readonly property `field: string` in the constructor alongside the error message.
   - Call `super(message)` first inside the constructor.
   - Set `this.name = "ValidationError"`.
   - Explicitly restore the prototype chain: `Object.setPrototypeOf(this, new.target.prototype);`.

2. Create a custom error class `NotFoundError extends Error`:
   - Include a public readonly property `resourceId: string` in the constructor.
   - Pass `"Resource not found: " + resourceId` to `super()`.
   - Set `this.name = "NotFoundError"`.
   - Explicitly restore the prototype chain: `Object.setPrototypeOf(this, new.target.prototype);`.

3. Write a function `getUserProfile(id: string, name: string): { id: string; name: string }` that:
   - Throws `new ValidationError("id", "User ID cannot be empty.")` if `id` is an empty string (`""`).
   - Throws `new ValidationError("name", "Name must be at least 2 characters.")` if `name.length < 2`.
   - Throws `new NotFoundError(id)` if `id !== "user-001"`.
   - Otherwise returns the user profile object: `{ id, name }`.

4. Write a helper function `safeGet(id: string, name: string): void` that wraps calls to `getUserProfile` in a `try / catch` block:
   - Use `instanceof ValidationError` to log: `"Validation failed on field '" + error.field + "': " + error.message`.
   - Use `instanceof NotFoundError` to log: `"Not found: " + error.resourceId`.
   - Use `instanceof Error` as a fallback to log: `"Unknown error: " + error.message`.

5. Call `safeGet` four times to test all execution paths:
   - Empty ID: `safeGet("", "Alice");`
   - Short Name: `safeGet("user-1", "A");`
   - Non-existent User: `safeGet("user-999", "Alice");`
   - Success Case: `safeGet("user-001", "Alice");`

## ANSWER HERE

```typescript
// Write your custom error classes, getUserProfile, safeGet, and test calls here
```
