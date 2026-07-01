# Challenge 02: Custom Error Classes

Build a typed error hierarchy and handle each type individually.

## Your Tasks

1. Create a class `ValidationError extends Error` with a `field: string` property in the constructor. Set `this.name = "ValidationError"`.

2. Create a class `NotFoundError extends Error` with a `resourceId: string` property. Set `this.name = "NotFoundError"`.

3. Write a function `getUserProfile(id: string, name: string): { id: string; name: string }` that:
   - Throws `new ValidationError("id", "User ID cannot be empty.")` if `id` is an empty string.
   - Throws `new ValidationError("name", "Name must be at least 2 characters.")` if `name.length < 2`.
   - Throws `new NotFoundError(id)` if `id !== "user-001"`.
   - Otherwise returns `{ id, name }`.

4. Call `getUserProfile` four times (once for each path: empty id, short name, not found, success). Wrap in `try/catch` using `instanceof` and log a different message for each error type.

## ANSWER HERE

```typescript
// Write your error classes and getUserProfile here:


```
