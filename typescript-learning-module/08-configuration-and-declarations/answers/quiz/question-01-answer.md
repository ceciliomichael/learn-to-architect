# Question 01 Answer

**What `strictNullChecks` forces TypeScript to do:**
It forces TypeScript to treat `null` and `undefined` as distinct types that are not automatically compatible with any other type. Without it, `null` can be assigned to any variable. With it, TypeScript tracks whether a value might be `null` or `undefined` and requires you to check before using it.

**Correct type for a nullable user:**
```typescript
let user: { name: string } | null = null;
```
Now TypeScript knows `user` might be `null` and will require a check before accessing `user.name`.

**Connection to optional chaining:**
Optional chaining (`?.`) exists precisely because of `strictNullChecks`. When a value might be `null` or `undefined`, accessing a property on it crashes the program. `?.` safely short-circuits the access and returns `undefined` instead of crashing. It is the safe alternative to: `user !== null && user !== undefined ? user.name : undefined`.
