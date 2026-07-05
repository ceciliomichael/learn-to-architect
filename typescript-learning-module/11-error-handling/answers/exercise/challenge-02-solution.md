# Challenge 02 Solution: Custom Error Classes & Prototype Restoration

## Executive Summary & Architectural Overview

In complex enterprise systems, throwing generic `new Error("message")` objects creates fragile architectures. When an application catches a generic error, the only way to determine *why* the failure occurred is by performing string matching on `error.message`. This is error-prone, breaks when error messages are modified or translated, and fails to carry typed metadata (such as the field name that failed validation or the ID of the missing resource).

To establish robust type-safe boundaries, senior engineers build custom domain error hierarchies that inherit from `Error`. This solution demonstrates how to design custom error classes in TypeScript, how to implement essential prototype chain restoration (`Object.setPrototypeOf`), and how to use `instanceof` to branch cleanly across different failure modes.

---

## Production-Grade Implementation

```typescript
/**
 * Base domain error for validation failures.
 * Carries the specific form or payload field name that failed validation.
 */
class ValidationError extends Error {
  public readonly field: string;

  constructor(field: string, message: string) {
    // Pass the message to the native Error constructor
    super(message);
    
    // Assign custom domain metadata
    this.field = field;
    
    // Explicitly set the error name for stack traces and logging tools
    this.name = "ValidationError";
    
    // CRITICAL TYPESCRIPT SYNTAX: Restore the prototype chain!
    // Without this, instanceof checks will fail when transpiled to ES5 / older targets.
    Object.setPrototypeOf(this, new.target.prototype);
  }
}

/**
 * Base domain error for missing resources.
 * Carries the specific resource identifier that could not be located.
 */
class NotFoundError extends Error {
  public readonly resourceId: string;

  constructor(resourceId: string) {
    super(`Resource not found: ${resourceId}`);
    this.resourceId = resourceId;
    this.name = "NotFoundError";
    
    // CRITICAL TYPESCRIPT SYNTAX: Restore the prototype chain!
    Object.setPrototypeOf(this, new.target.prototype);
  }
}

/**
 * Retrieves a user profile by ID and Name, validating domain rules.
 * Throws typed domain errors upon failure.
 */
function getUserProfile(id: string, name: string): { id: string; name: string } {
  // Rule 1: ID cannot be empty
  if (id.trim().length === 0) {
    throw new ValidationError("id", "User ID cannot be empty.");
  }
  
  // Rule 2: Name must be at least 2 characters long
  if (name.trim().length < 2) {
    throw new ValidationError("name", "Name must be at least 2 characters long.");
  }
  
  // Rule 3: Simulate database check - only user-001 exists in our store
  if (id !== "user-001") {
    throw new NotFoundError(id);
  }
  
  return { id, name };
}

/**
 * Wraps profile retrieval in a safe execution boundary.
 * Uses instanceof to branch cleanly and log domain-specific formatting.
 */
function safeGet(id: string, name: string): void {
  try {
    const profile = getUserProfile(id, name);
    console.log(`[SUCCESS]: Found profile for ${profile.name} (ID: ${profile.id})`);
  } catch (error: unknown) {
    // Gate 1: Check if the failure was a domain validation error
    if (error instanceof ValidationError) {
      // TypeScript automatically narrows 'error' to ValidationError!
      // We can safely access error.field and error.message!
      console.warn(`[VALIDATION FAILED]: Field '${error.field}' -> ${error.message}`);
    } 
    // Gate 2: Check if the failure was a missing resource error
    else if (error instanceof NotFoundError) {
      // TypeScript automatically narrows 'error' to NotFoundError!
      // We can safely access error.resourceId!
      console.warn(`[NOT FOUND]: Could not locate record with ID '${error.resourceId}'.`);
    } 
    // Gate 3: Fallback for generic or unexpected system errors
    else if (error instanceof Error) {
      console.error(`[SYSTEM ERROR]: Unexpected failure -> ${error.message}`);
    } 
    // Gate 4: Fallback for non-error primitives
    else {
      console.error("[CRITICAL]: Unrecognized non-error exception thrown:", error);
    }
  }
}

// ==========================================
// Verification & Test Executions
// ==========================================

console.log("--- Test 1: Empty ID Validation Failure ---");
safeGet("", "Alice"); // Triggers ValidationError on 'id'

console.log("\n--- Test 2: Short Name Validation Failure ---");
safeGet("user-1", "A"); // Triggers ValidationError on 'name'

console.log("\n--- Test 3: Resource Not Found Failure ---");
safeGet("user-999", "Alice"); // Triggers NotFoundError on 'user-999'

console.log("\n--- Test 4: Successful Retrieval ---");
safeGet("user-001", "Alice"); // Succeeds and returns profile
```

---

## Symbol-by-Symbol Breakdown

1. **`class ValidationError extends Error`**: Declares a custom class that inherits all properties and methods from JavaScript's built-in `Error` class (including `.message` and `.stack`).
2. **`super(message)`**: Invokes the constructor of the parent `Error` class. In JavaScript/TypeScript class inheritance, calling `super()` is mandatory before accessing `this` inside a subclass constructor.
3. **`this.name = "ValidationError"`**: Overrides the default error name property. By default, `Error.prototype.name` is set to `"Error"`. Setting `this.name` ensures that stack traces, error logging utilities (like Sentry or Winston), and `.toString()` outputs display `"ValidationError: ..."` instead of generic `"Error: ..."`.
4. **`Object.setPrototypeOf(this, new.target.prototype)`**: The critical prototype restoration line. `new.target` refers directly to the constructor function that was invoked with the `new` keyword (in this case, `ValidationError` or `NotFoundError`). This line explicitly binds the instance's internal `[[Prototype]]` link to the custom class prototype.
5. **`if (error instanceof ValidationError)`**: The runtime type guard. The `instanceof` operator checks whether `ValidationError.prototype` exists anywhere in the prototype chain of the `error` object. When true, the TypeScript compiler unlocks domain properties (`error.field`).

---

## Deep Dive: Why `Object.setPrototypeOf` is Required in TypeScript

To understand why `Object.setPrototypeOf(this, new.target.prototype)` is mandatory in TypeScript, we must examine how JavaScript JavaScript engines and TypeScript transpilers handle built-in constructors (`Error`, `Array`, `Map`).

### The ES5 Transpilation Problem
When TypeScript transpiles ES6 classes down to ES5 (for compatibility with older runtimes or legacy environments), class inheritance is modeled using standard constructor functions and prototype chaining:

```javascript
// Transpiled ES5 representation of extending Error
function ValidationError(field, message) {
  // In ES5, super(message) is compiled to a function call on Error:
  var _this = Error.call(this, message) || this;
  _this.field = field;
  _this.name = "ValidationError";
  return _this;
}
ValidationError.prototype = Object.create(Error.prototype);
```

### Why `instanceof` Fails Without Restoration
In JavaScript engines, built-in constructors like `Error()` and `Array()` are special: when invoked via `Error.call(this, message)`, the built-in constructor ignores the passed `this` context and allocates a brand new `Error` object in memory whose prototype is strictly bound to `Error.prototype` (not `ValidationError.prototype`!).

When the constructor finishes, the returned object has its prototype pointing directly to `Error.prototype`!
Therefore, when calling code executes:
```typescript
const err = new ValidationError("email", "Invalid email format");
console.log(err instanceof ValidationError); // RETURNS FALSE IN ES5 WITHOUT RESTORATION!
console.log(err instanceof Error);           // Returns true
```
Because the internal prototype link was severed during the built-in `Error` constructor call, `err instanceof ValidationError` evaluates to **`false`**, causing your exception handling logic to silently bypass your custom error gates!

By executing **`Object.setPrototypeOf(this, new.target.prototype)`**, you manually force the newly allocated error instance to point back to your subclass prototype, guaranteeing 100% reliable `instanceof` behavior across all JavaScript runtime targets!

---

## Architectural Trade-offs: Error Hierarchies vs. Error Codes vs. Generic Strings

| Architectural Approach | Advantages | Disadvantages | When to Use |
| :--- | :--- | :--- | :--- |
| **Custom Error Hierarchies** (`class NotFoundError extends Error`) | Unlocks language-level `instanceof` type narrowing; allows attaching strongly-typed domain properties (`field`, `resourceId`, `httpStatus`); self-documenting code. | Requires defining boilerplate classes for each domain error; requires careful prototype restoration (`Object.setPrototypeOf`). | Enterprise backend services, REST/GraphQL API controllers, complex domain models, and core libraries. |
| **Numeric or String Error Codes** (`throw new Error("ERR_NOT_FOUND: user-999")` or `{ code: 404 }`) | Easy to serialize across network boundaries (JSON payloads); simple to store in logs or databases without class instantiation. | Lacks type safety; requires parsing strings or checking code properties manually; does not benefit from TypeScript union narrowing. | Lightweight microservices, simple network RPC protocols, or legacy codebase integrations. |
| **Generic Strings / Errors** (`throw new Error("User not found")`) | Zero setup cost; fast to implement for quick prototypes or simple scripts. | **Brittle Anti-Pattern in Production:** Callers cannot distinguish error types without string matching; breaks when messages change or are localized. | Never use for domain logic in production; acceptable only for rapid prototyping or fatal startup crashes. |

---

## Concrete Anti-Patterns vs. Best Practices

### 1. Distinguishing Errors via String Matching (The Brittle Anti-Pattern)
```typescript
// ANTI-PATTERN: String matching on error messages!
try {
  getUserProfile(id, name);
} catch (error: any) {
  // If a developer fixes a typo in the error message, this logic breaks!
  if (error.message.includes("not found")) {
    show404Page();
  } else if (error.message.includes("cannot be empty")) {
    showFormError();
  }
}

// BEST PRACTICE: Precise class narrowing via instanceof
try {
  getUserProfile(id, name);
} catch (error: unknown) {
  if (error instanceof NotFoundError) {
    show404Page(error.resourceId); // Typed metadata!
  } else if (error instanceof ValidationError) {
    showFormError(error.field, error.message); // Typed metadata!
  }
}
```

### 2. Omitting `this.name` in Custom Errors
```typescript
// ANTI-PATTERN: Forgetting to set this.name
class DatabaseError extends Error {
  constructor(query: string) {
    super(`Query failed: ${query}`);
    // this.name is omitted! It remains "Error" by default!
  }
}
const err = new DatabaseError("SELECT *");
console.log(err.toString()); // Outputs: "Error: Query failed: SELECT *" (Misleading!)

// BEST PRACTICE: Always explicitly assign this.name
class DatabaseError extends Error {
  constructor(query: string) {
    super(`Query failed: ${query}`);
    this.name = "DatabaseError";
    Object.setPrototypeOf(this, new.target.prototype);
  }
}
const errBest = new DatabaseError("SELECT *");
console.log(errBest.toString()); // Outputs: "DatabaseError: Query failed: SELECT *" (Clear!)
```

### 3. Omitting Prototype Restoration
```typescript
// ANTI-PATTERN: Omitting Object.setPrototypeOf
class AuthError extends Error {
  constructor(message: string) {
    super(message);
    this.name = "AuthError";
    // Omitting Object.setPrototypeOf causes instanceof checks to fail in transpiled code!
  }
}

// BEST PRACTICE: Always include prototype restoration
class AuthError extends Error {
  constructor(message: string) {
    super(message);
    this.name = "AuthError";
    Object.setPrototypeOf(this, new.target.prototype); // 100% reliable!
  }
}
```
