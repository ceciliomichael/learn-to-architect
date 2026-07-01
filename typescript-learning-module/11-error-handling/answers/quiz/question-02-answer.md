# Question 02 Answer

**Scenario 1  -  `try` completes normally:**
Yes, `finally` runs. After the last line of `try` executes, control passes to `finally`, then continues normally.

**Scenario 2  -  `try` throws and `catch` handles it:**
Yes, `finally` runs. After `catch` finishes handling the error, control passes to `finally`.

**Scenario 3  -  `try` throws and there is no `catch` block:**
Yes, `finally` still runs. The error will propagate up the call stack after `finally` completes, but `finally` will always execute first. This is useful for resource cleanup even during unhandled errors.

**Scenario 4  -  `return` inside `try`:**
Yes, `finally` runs. JavaScript intercepts the `return` statement, runs the `finally` block, and then the return happens. If `finally` itself contains a `return`, it overrides the `try`'s return value.

**Scenario 5  -  `return` inside `catch`:**
Yes, `finally` runs. Same behavior as Scenario 4. The `return` in `catch` is deferred until after `finally` completes.

The takeaway: `finally` runs in every case, no matter what. This makes it reliable for cleanup tasks like closing connections or releasing resources.
