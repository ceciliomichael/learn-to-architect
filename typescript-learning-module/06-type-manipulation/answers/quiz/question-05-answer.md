# Question 05  -  Answer: Combining Utility Types

## Question Recap

> You need a type that removes `id` and `createdAt` from `User` and makes everything else optional. Write the single combined utility type expression.

---

## Answer

```typescript
interface User {
  id: string;
  username: string;
  email: string;
  passwordHash: string;
  createdAt: Date;
}

// Combined utility type expression:
type UserDraft = Partial<Omit<User, 'id' | 'createdAt'>>;

// Resolves to:
// {
//   username?: string;
//   email?: string;
//   passwordHash?: string;
// }
```

---

## Explanation

The expression chains two utility types:

1. **`Omit<User, 'id' | 'createdAt'>`**  -  produces an intermediate type with `id` and `createdAt` removed:
   ```
   { username: string; email: string; passwordHash: string; }
   ```

2. **`Partial<...>`**  -  wraps the result and makes every remaining property optional:
   ```
   { username?: string; email?: string; passwordHash?: string; }
   ```

### Order Matters

- `Partial<Omit<User, ...>>` → remove first, then make optional. ✅ Correct and most readable.
- `Omit<Partial<User>, ...>` → make all optional first, then remove. Also produces the same result here, but reads less naturally.

### Real-World Use Case

This exact pattern is used for **form state** and **PATCH request bodies**  -  you want to send only the fields the user actually changed, `id` is assigned by the server, and `createdAt` is set automatically:

```typescript
async function patchUser(id: string, changes: UserDraft): Promise<void> {
  await fetch(`/api/users/${id}`, {
    method: 'PATCH',
    body: JSON.stringify(changes),
  });
}

// Valid  -  only sending changed fields
await patchUser('u-001', { email: 'new@example.com' });
```
