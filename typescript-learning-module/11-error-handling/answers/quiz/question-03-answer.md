# Question 03 Answer

**Problem with Approach A (how does the caller distinguish errors?):**
With `new Error("User not found: ...")`, the only way to distinguish it from a `ValidationError` is to parse the error message string  -  checking if it contains certain words. This is fragile. The message could change, be translated, or have a typo. String-matching error messages is a bad practice that leads to brittle, error-prone code.

**How `instanceof` solves it:**
With custom error classes, each error type has a unique class identity. `instanceof` checks the class of the object, not its message. This is precise and language-level
```typescript
if (error instanceof NotFoundError) {
  console.log("Missing:", error.resourceId); // Access typed properties.
} else if (error instanceof ValidationError) {
  console.log("Bad field:", error.field);
}
```
Each custom error can also carry typed extra data (like `field` or `resourceId`) that a plain `new Error()` cannot.

**Purpose of setting `this.name`:**
JavaScript's Error class sets `name` to `"Error"` by default. If you extend it and do not set `this.name`, the error's name in stack traces and `toString()` output will still show `"Error"` instead of `"NotFoundError"`. Setting `this.name` ensures that logging and debugging tools correctly identify your custom error type.
