# Module 11: Error Handling

Every program that interacts with the real world encounters errors: network failures, invalid user input, missing files, database timeouts. This module teaches you how to handle errors properly in TypeScript so your program fails gracefully instead of crashing unexpectedly.

---

## 1. What is an Error?

An **error** (also called an **exception**) is an event that disrupts the normal flow of your program. If left unhandled, an error crashes your program with a message in the terminal or browser console.

In JavaScript and TypeScript, errors are thrown using the `throw` keyword and caught using `try/catch` blocks.

---

## 2. `try`, `catch`, `finally`

This is the fundamental error handling structure. You put risky code inside `try`. If anything inside `try` throws an error, execution immediately jumps to `catch`. The `finally` block (optional) always runs at the end, whether or not an error occurred:

```typescript
function divide(a: number, b: number): number {
  if (b === 0) {
    throw new Error("Cannot divide by zero."); // Throws an error object.
  }
  return a / b;
}

try {
  const result = divide(10, 0); // This line will throw.
  console.log(result);          // This line never runs if divide throws.
} catch (error) {
  // Execution jumps here when an error is thrown.
  console.log("Something went wrong.");
} finally {
  // This block ALWAYS runs, error or not. Used for cleanup.
  console.log("Done attempting the division.");
}
```

Output:
```
Something went wrong.
Done attempting the division.
```

### When Does `finally` Run?

`finally` runs in every case:
- When `try` completes normally without any error.
- When `catch` handles an error.
- Even when a `return` statement is inside `try` or `catch`.

It is commonly used to release resources: closing a database connection, stopping a loading spinner, or clearing a timer.

---

## 3. The `Error` Object

JavaScript has a built-in `Error` class. When you create one with `new Error("some message")`, it holds:
- `message`: The text you provided.
- `name`: The name of the error type (`"Error"` by default).
- `stack`: A trace showing which lines of code were running when the error occurred (useful for debugging).

```typescript
const err = new Error("Something failed.");
console.log(err.message); // "Something failed."
console.log(err.name);    // "Error"
```

---

## 4. Typing the `catch` Variable

In TypeScript's strict mode, the variable inside `catch` is typed as `unknown` by default. This forces you to check what the error is before using it. This is safer than JavaScript, which types it as `any`:

```typescript
try {
  throw new Error("Network timeout.");
} catch (error) {
  // error is 'unknown'. You cannot access error.message directly.
  if (error instanceof Error) {
    // Inside this block, TypeScript knows 'error' is an Error object.
    console.log("Error message:", error.message);
  } else {
    // Someone might have thrown a non-Error value like: throw "string error";
    console.log("Unknown error type:", error);
  }
}
```

The `instanceof` operator checks whether an object was created from a specific class. `error instanceof Error` asks: "Was this error created using the `Error` class or one of its subclasses?"

---

## 5. Custom Error Classes

Throwing a generic `Error` is fine for simple cases. For larger applications, you want specific error types so you can handle different failure modes differently. You create custom errors by extending the built-in `Error` class:

```typescript
class ValidationError extends Error {
  constructor(public field: string, message: string) {
    super(message); // Call the parent Error constructor with the message.
    this.name = "ValidationError"; // Set a distinct name for this error type.
  }
}

class NotFoundError extends Error {
  constructor(public resourceId: string) {
    super("Resource not found: " + resourceId);
    this.name = "NotFoundError";
  }
}
```

Now you can throw and catch specific error types:

```typescript
function getUserById(id: string): { id: string; name: string } {
  if (id === "") {
    throw new ValidationError("id", "User ID cannot be empty.");
  }
  if (id !== "user-1") {
    throw new NotFoundError(id);
  }
  return { id: "user-1", name: "Alice" };
}

try {
  const user = getUserById("unknown-id");
} catch (error) {
  if (error instanceof ValidationError) {
    console.log("Validation failed on field:", error.field);
    console.log("Message:", error.message);
  } else if (error instanceof NotFoundError) {
    console.log("Could not find resource:", error.resourceId);
    console.log("Message:", error.message);
  } else if (error instanceof Error) {
    console.log("Unexpected error:", error.message);
  }
}
```

This pattern is far superior to throwing plain strings or checking error messages with string comparisons.

---

## 6. Error Handling in Async Functions

In async functions, a rejected Promise behaves like a thrown error when you use `await`. You handle it exactly the same way with `try/catch`:

```typescript
interface Post {
  id: number;
  title: string;
}

async function fetchPost(id: number): Promise<Post> {
  // Simulating a failed network request:
  if (id <= 0) {
    throw new ValidationError("id", "Post ID must be a positive number.");
  }
  // Simulating a successful result:
  return { id, title: "Hello TypeScript" };
}

async function loadPost(id: number): Promise<void> {
  try {
    const post = await fetchPost(id); // If fetchPost throws, jump to catch.
    console.log("Loaded post:", post.title);
  } catch (error) {
    if (error instanceof ValidationError) {
      console.log("Bad input:", error.message);
    } else if (error instanceof Error) {
      console.log("Request failed:", error.message);
    }
  } finally {
    console.log("Request attempt finished.");
  }
}

loadPost(-1);  // Will trigger ValidationError.
loadPost(5);   // Will succeed.
```

---

## 7. The Result Pattern: Errors as Data

A popular alternative to `try/catch` is modeling success and failure as a typed union. Instead of throwing errors, your function returns an object that is either a success with data or a failure with an error message. This avoids the surprising control flow of exceptions:

```typescript
type Result<T> =
  | { success: true; data: T }
  | { success: false; error: string };

function parseName(input: string): Result<string> {
  if (input.trim().length === 0) {
    return { success: false, error: "Name cannot be empty." };
  }
  return { success: true, data: input.trim() };
}

const result = parseName("  Alice  ");

if (result.success) {
  console.log("Name is:", result.data); // TypeScript knows 'data' exists here.
} else {
  console.log("Error:", result.error); // TypeScript knows 'error' exists here.
}
```

This is a discriminated union (covered in Module 04) applied to error handling. The caller is forced by TypeScript to handle both the success and failure case.

---

## 8. Rethrowing Errors

Sometimes you want to catch an error to check it, but if it is not the type you expected, you want to let it propagate up the call stack to be handled by a parent function. You do this by rethrowing:

```typescript
async function processOrder(orderId: string): Promise<void> {
  try {
    await submitOrder(orderId);
  } catch (error) {
    if (error instanceof ValidationError) {
      // We know how to handle this. Log it and stop.
      console.log("Order validation failed:", error.message);
      return;
    }
    // We do not know what this error is. Pass it up.
    throw error;
  }
}
```

This keeps error handling close to where errors make sense. Errors you understand get handled; everything else gets passed up.

---

## 9. Never Swallow Errors Silently

One of the most dangerous things in any codebase is an empty `catch` block:

```typescript
// BAD: This hides bugs and makes debugging nearly impossible.
try {
  riskyOperation();
} catch (error) {
  // Nothing here. The error disappears silently.
}
```

At minimum, always log the error. Even if you cannot recover from it, logging ensures you can see what went wrong:

```typescript
// GOOD: Always acknowledge the error even if you cannot fix it.
try {
  riskyOperation();
} catch (error) {
  console.error("Unexpected error in riskyOperation:", error);
}
```

---

## 10. Summary: When to Use What

| Situation | Recommended Approach |
|---|---|
| A function can fail in predictable ways | Return a `Result<T>` union |
| A function requires valid inputs | Throw a `ValidationError` |
| A resource does not exist | Throw a `NotFoundError` |
| A network or I/O failure | `try/catch` with `instanceof` checks |
| Multiple async tasks that might fail | `Promise.allSettled` |
| You receive an unknown error type | Check `instanceof Error` before accessing `.message` |
| You want to re-use a resource after failure | Use `finally` for cleanup |
