# Question 01 Answer

**Three states:**
1. **Pending**  -  The async operation has started but has not yet produced a result. The Promise is still "in progress."
2. **Fulfilled**  -  The operation completed successfully. The Promise now holds the resolved value, which is delivered to any `.then()` callbacks or `await` expressions.
3. **Rejected**  -  The operation failed. The Promise now holds the rejection reason (usually an `Error` object), which is delivered to any `.catch()` callbacks or triggers the `catch` block of a `try/catch`.

**Can a settled Promise change state?**
No. A Promise is immutable once it leaves the pending state. Once fulfilled, it stays fulfilled. Once rejected, it stays rejected. There is no way to reset it. A new Promise must be created for a new attempt.

**Attaching callbacks after the Promise has already settled:**
They still work. If you attach a `.then()` callback to a Promise that has already fulfilled, the callback runs immediately (asynchronously, in the next microtask). The callback does not miss the result just because it was attached after the fact.
