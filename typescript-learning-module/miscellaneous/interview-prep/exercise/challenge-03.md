# Challenge 03: Async Resilience & The Result Pattern

In distributed backend systems, calling external services can fail independently. Seniors never let one failed request abort an entire batch operation.

## Your Tasks

1. Define a generic `Result<T, E = string>` discriminated union with `{ success: true; data: T }` and `{ success: false; error: E }`.

2. Write an async helper function `safeExec<T>(promise: Promise<T>): Promise<Result<T, string>>` that awaits any promise inside a `try/catch` block. On fulfillment, it returns `{ success: true, data }`. On rejection, it checks `instanceof Error` and returns `{ success: false, error: error.message }` (or `"Unknown error"`).

3. Suppose you have 3 simulated external API endpoints
   - `fetchUserProfile(userId: string): Promise<{ id: string; name: string }>` (resolves in 100ms)
   - `fetchUserBalance(userId: string): Promise<number>` (resolves in 150ms)
   - `fetchUserNotifications(userId: string): Promise<string[]>` (rejects with `new Error("Notification service offline")` after 120ms)

4. Write an async function `getDashboardData(userId: string): Promise<{ profile: Result<{ id: string; name: string }>; balance: Result<number>; notifications: Result<string[]> }>` that fires all 3 requests **concurrently in parallel** using `Promise.all` wrapped around your `safeExec` helper.

5. Call `getDashboardData("user-99")` and log the output. Verify that even though notifications failed, profile and balance successfully returned data in parallel without throwing an unhandled exception
## ANSWER HERE

```typescript
// Write Result<T, E>, safeExec, the mock APIs, and getDashboardData here
```
