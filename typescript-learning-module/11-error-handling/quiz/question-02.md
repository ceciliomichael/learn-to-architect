# Question 02: When Does finally Run?

The `finally` block in a `try / catch / finally` statement is engineered to provide reliable resource cleanup (such as closing database connections, closing file descriptors, or releasing mutex locks). A common developer adage states that "the `finally` block always runs after `try` and `catch`."

But does "always" truly mean in *every conceivable execution path*?

For each of the five runtime scenarios below, state clearly whether the `finally` block executes, and explain the exact call stack behavior and control flow mechanics:

1. **Scenario 1:** The `try` block completes normally without throwing any error.
2. **Scenario 2:** The `try` block throws an exception, and the `catch` block successfully intercepts and handles it.
3. **Scenario 3:** The `try` block throws an exception, but there is no `catch` block attached (only `try / finally`).
4. **Scenario 4:** There is an explicit `return` statement executed inside the `try` block.
5. **Scenario 5:** There is an explicit `return` statement executed inside the `catch` block.

## ANSWER HERE

> **Scenario 1 (try completes normally):**

> **Scenario 2 (try throws, catch handles):**

> **Scenario 3 (try throws, no catch block):**

> **Scenario 4 (explicit return inside try block):**

> **Scenario 5 (explicit return inside catch block):**
