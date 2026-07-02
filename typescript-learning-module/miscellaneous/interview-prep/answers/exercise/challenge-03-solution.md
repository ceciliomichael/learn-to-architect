# Solution  -  Challenge 03: Async Resilience & The Result Pattern

## Full Production Implementation

```typescript
// 1. Generic Result Discriminated Union
export type Result<T, E = string> =
  | { success: true; data: T }
  | { success: false; error: E };

// 2. Safe Execution Wrapper
export async function safeExec<T>(promise: Promise<T>): Promise<Result<T, string>> {
  try {
    const data = await promise;
    return { success: true, data };
  } catch (err: unknown) {
    const message = err instanceof Error ? err.message : String(err);
    return { success: false, error: message };
  }
}

// 3. Mock APIs
async function fetchUserProfile(userId: string): Promise<{ id: string; name: string }> {
  return new Promise((resolve) => setTimeout(() => resolve({ id: userId, name: "Alice" }), 100));
}

async function fetchUserBalance(userId: string): Promise<number> {
  return new Promise((resolve) => setTimeout(() => resolve(4250.75), 150));
}

async function fetchUserNotifications(userId: string): Promise<string[]> {
  return new Promise((_, reject) => setTimeout(() => reject(new Error("Notification service offline")), 120));
}

// 4. Parallel Concurrent Dashboard Aggregator
export async function getDashboardData(userId: string): Promise<{
  profile: Result<{ id: string; name: string }>;
  balance: Result<number>;
  notifications: Result<string[]>;
}> {
  // Fire all 3 concurrently in parallel. safeExec prevents Promise.all from short-circuiting
  const [profile, balance, notifications] = await Promise.all([
    safeExec(fetchUserProfile(userId)),
    safeExec(fetchUserBalance(userId)),
    safeExec(fetchUserNotifications(userId)),
  ]);

  return { profile, balance, notifications };
}

// 5. Execution Test
async function runDemo() {
  const dashboard = await getDashboardData("user-99");
  console.log(JSON.stringify(dashboard, null, 2));
  /* Output
  {
    "profile": { "success": true, "data": { "id": "user-99", "name": "Alice" } },
    "balance": { "success": true, "data": 4250.75 },
    "notifications": { "success": false, "error": "Notification service offline" }
  }
  */
}
```
