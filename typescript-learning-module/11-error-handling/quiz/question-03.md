# Question 03: Custom Error Classes

Why create custom error classes instead of always throwing `new Error("some message")`?

```typescript
// Approach A: generic error
throw new Error("User not found: user-999");

// Approach B: custom error class
class NotFoundError extends Error {
  constructor(public resourceId: string) {
    super("Resource not found: " + resourceId);
    this.name = "NotFoundError";
  }
}
throw new NotFoundError("user-999");
```

1. How does the caller handle Approach A if it also needs to handle a `ValidationError` differently?
2. How does `instanceof` solve this problem with Approach B?
3. What is the purpose of setting `this.name` inside a custom error constructor?

## ANSWER HERE

> **Problem with Approach A (how does the caller distinguish errors?):**

> **How instanceof solves it:**

> **Purpose of setting this.name:**
