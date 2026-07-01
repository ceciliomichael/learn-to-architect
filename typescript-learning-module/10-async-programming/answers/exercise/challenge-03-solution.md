# Challenge 03: Solution

```typescript
async function fetchUser(id: number): Promise<{ id: number; name: string }> {
  return new Promise((resolve) => setTimeout(() => resolve({ id, name: "Alice" }), 400));
}

async function fetchUserPosts(userId: number): Promise<string[]> {
  return new Promise((resolve) =>
    setTimeout(() => resolve(["Post A", "Post B", "Post C"]), 300)
  );
}

async function loadUserDashboard(userId: number): Promise<void> {
  // Both tasks start at the same time:
  // Sequential would take: 400ms + 300ms = 700ms total
  // Parallel takes:        max(400ms, 300ms) = 400ms total

  const [user, posts] = await Promise.all([
    fetchUser(userId),
    fetchUserPosts(userId)
  ]);

  console.log("Dashboard for " + user.name + ": " + posts.length + " posts");
  // "Dashboard for Alice: 3 posts"
}

loadUserDashboard(1);
```
