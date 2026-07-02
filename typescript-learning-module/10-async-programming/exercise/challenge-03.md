# Challenge 03: Parallel Requests with Promise.all

Practice running multiple async tasks at the same time.

## Starting Functions

Write these two simulator functions first (they are given to you)
```typescript
async function fetchUser(id: number): Promise<{ id: number; name: string }> {
  return new Promise((resolve) => setTimeout(() => resolve({ id, name: "Alice" }), 400));
}

async function fetchUserPosts(userId: number): Promise<string[]> {
  return new Promise((resolve) =>
    setTimeout(() => resolve(["Post A", "Post B", "Post C"]), 300)
  );
}
```

## Your Tasks

1. Write an async function `loadUserDashboard(userId: number): Promise<void>` that uses `Promise.all` to fetch both the user and their posts simultaneously.
2. After both resolve, log: `"Dashboard for " + user.name + ": " + posts.length + " posts"`.
3. Add a comment calculating the total time: sequential would take 700ms (400 + 300), parallel takes only 400ms (the maximum of the two).

## ANSWER HERE

```typescript
async function fetchUser(id: number): Promise<{ id: number; name: string }> {
  return new Promise((resolve) => setTimeout(() => resolve({ id, name: "Alice" }), 400));
}

async function fetchUserPosts(userId: number): Promise<string[]> {
  return new Promise((resolve) =>
    setTimeout(() => resolve(["Post A", "Post B", "Post C"]), 300)
  );
}

// Write loadUserDashboard here
```
