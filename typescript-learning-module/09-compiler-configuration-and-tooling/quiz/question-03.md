# Question 03: Array Safety and noUncheckedIndexedAccess

In standard JavaScript, accessing an array index or dictionary key that does not exist fails silently at runtime, returning `undefined` instead of throwing an out-of-bounds exception. This behavior creates a significant safety gap when modeled in TypeScript.

## Conceptual Questions

1. Consider the following code snippet:
   ```typescript
   const userRoles: string[] = ["Admin", "Editor"];
   const selectedRole = userRoles[99];
   ```
   If `"noUncheckedIndexedAccess"` is set to **false** (the default in standard TypeScript), what exact type does the compiler assign to `selectedRole`? Why is this inferred type fundamentally dishonest about runtime reality?
2. What happens when you enable `"noUncheckedIndexedAccess": true` in your `tsconfig.json`? What new type is inferred for `selectedRole`?
3. How does this setting force developers to change their coding patterns when working with arrays, loops, and dynamic record lookups? Describe at least two techniques for safely working with indexed elements under this strict rule.

---

## ANSWER HERE

> **1. Inferred Type and Dishonesty under Default Settings:**

> **2. Type Transformation under `"noUncheckedIndexedAccess": true`:**

> **3. Impact on Coding Patterns and Safe Access Techniques:**
