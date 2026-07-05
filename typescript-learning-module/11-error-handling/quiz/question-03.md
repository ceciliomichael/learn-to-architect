# Question 03: Custom Error Classes & Prototype Mechanics

When building enterprise applications, junior developers often throw generic error objects with descriptive strings: `throw new Error("User not found: user-999")`. Senior architects, however, design custom domain error hierarchies that extend the native `Error` class.

Consider the two approaches below:

```typescript
// Approach A: Generic error with string formatting
throw new Error("User not found: user-999");

// Approach B: Custom domain error class
class NotFoundError extends Error {
  constructor(public resourceId: string) {
    super("Resource not found: " + resourceId);
    this.name = "NotFoundError";
    Object.setPrototypeOf(this, new.target.prototype);
  }
}
throw new NotFoundError("user-999");
```

Please answer the following four architectural questions:

1. **How does calling code handle Approach A if it also needs to handle a `ValidationError` differently?** Why is string-matching on `error.message` considered an anti-pattern?
2. **How does `instanceof` solve this branching problem in Approach B?** What type-narrowing benefits does TypeScript provide inside an `if (error instanceof NotFoundError)` block?
3. **What is the purpose of explicitly setting `this.name = "NotFoundError"` inside the custom error constructor?** What happens in logging tools or stack traces if you omit this line?
4. **Why is `Object.setPrototypeOf(this, new.target.prototype)` essential syntax in TypeScript when extending `Error`?** What JavaScript prototype chain issue occurs when transpiling classes to ES5 without this line?

## ANSWER HERE

> **1. Problem with Approach A (distinguishing errors via string matching):**

> **2. How instanceof solves the branching problem in Approach B:**

> **3. Purpose of setting this.name in the constructor:**

> **4. Why Object.setPrototypeOf is required when extending Error in TypeScript:**
