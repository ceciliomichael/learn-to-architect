# Question 01 Answer

**Why `error` is `unknown`:**
In theory, anyone can `throw` anything in JavaScript  -  a string, a number, a plain object, or an `Error` instance. TypeScript cannot guarantee that what was thrown is an `Error` object. In strict mode, TypeScript types the `catch` variable as `unknown` to force you to verify what it actually is before using it. Accessing `.message` on something that might not be an `Error` would be unsafe.

**What you must do before accessing `.message`:**
Check if `error` is an instance of `Error` using `instanceof`.

**Corrected catch block:**
```typescript
catch (error) {
  if (error instanceof Error) {
    console.log(error.message); // Safe  -  TypeScript narrows to Error.
  } else {
    console.log("A non-Error value was thrown:", error);
  }
}
```
