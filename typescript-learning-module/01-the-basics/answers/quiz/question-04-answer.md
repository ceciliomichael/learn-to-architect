# Question 04 Answer

**For `any`  -  calling `.explode()`:**
TypeScript produces no error. `any` disables all type checking for that variable. TypeScript trusts you completely and allows any method call, any property access, and any assignment. The code compiles successfully. But at runtime, calling `.explode()` on a string will crash the program because strings do not have an `explode` method.

**For `unknown`  -  calling `.explode()`:**
TypeScript produces an error: `Object is of type 'unknown'`. The compiler blocks you from calling any method or accessing any property on an `unknown` variable until you first prove what type it is using a narrowing check.

**Which to prefer:**
Always prefer `unknown`. It forces you to be deliberate about what you do with uncertain data, which catches bugs at compile time instead of at runtime.

**What you must do before using `unknown`:**
Narrow the type using a `typeof` check inside an `if` statement
```typescript
let valueB: unknown = "hello";
if (typeof valueB === "string") {
  valueB.toUpperCase(); // Safe  -  TypeScript knows it is a string here.
}
```
