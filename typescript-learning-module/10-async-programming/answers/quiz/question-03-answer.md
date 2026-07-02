# Question 03 Answer

**Sequential  -  total time and why:**
2 seconds (1 + 1). The second `await` only starts after the first `await` has completely resolved. The program waits for `fetchA` to finish before it even starts `fetchB`. The wait times add together.

**Parallel  -  total time and why:**
1 second (the maximum of the two). `Promise.all` starts both `fetchA()` and `fetchB()` at exactly the same time. While `fetchA` is waiting its 1 second, `fetchB` is also running its 1 second simultaneously. Both finish at roughly the same moment. You wait for the slowest one, not the sum of all.

**When NOT to use Promise.all:**
When the second task depends on the result of the first task. For example
```typescript
const user    = await fetchUser(userId);       // Must finish first.
const profile = await fetchProfile(user.role); // Needs user.role from above.
```
You cannot start `fetchProfile` until you know `user.role`, so they must run sequentially. `Promise.all` is only safe when tasks are completely independent of each other.
