# Question 05: Return Type Annotations for Async Functions

**What is the correct return type annotation for an async function that fetches a `User` object and returns it?**

**What about an async function that just logs something and returns nothing?**

---

Given this interface
```typescript
interface User {
  id: number;
  username: string;
  email: string;
}
```

**Answer the following:**

1. Write the correct return type for an async function `getUser` that fetches and returns a `User`.
2. Write the correct return type for an async function `logUser` that logs a user's name and returns nothing meaningful.
3. Why is it **wrong** to annotate an async function as returning `User` directly (without `Promise<...>`)?
4. **Bonus**: What does TypeScript do if you write `return "hello"` inside a function annotated as `Promise<number>`?

---

## Answer

```
// ANSWER HERE
```
