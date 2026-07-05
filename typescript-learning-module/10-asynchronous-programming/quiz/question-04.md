# Question 04: `Promise.all` vs `Promise.allSettled`

**What is the difference between `Promise.all` and `Promise.allSettled`?**

**When would you choose `Promise.allSettled` over `Promise.all`?**

---

Given these two Promises
```typescript
const p1 = fetchUser(1);    // succeeds
const p2 = fetchUser(999);  // rejects with Error('User not found')
```

**Answer the following:**

1. What happens when you `await Promise.all([p1, p2])`? What do you get back?
2. What happens when you `await Promise.allSettled([p1, p2])`? What shape does the result have?
3. Give a **real-world scenario** where `Promise.allSettled` is the better choice.

---

## Answer

```
// ANSWER HERE
```
