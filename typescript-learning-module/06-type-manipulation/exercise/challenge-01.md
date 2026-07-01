# Challenge 01: Reshaping a User Type with Utility Types

Practice deriving multiple types from one source interface without repeating yourself.

## Starting Interface

```typescript
interface User {
  id: string;
  username: string;
  email: string;
  passwordHash: string;
  createdAt: Date;
}
```

## Your Tasks

Using only utility types (no manual re-typing of properties), create these four type aliases:

1. `UserUpdatePayload`: All fields optional, but `id` and `createdAt` are removed entirely.
2. `PublicUser`: Only `id`, `username`, and `email` (removes sensitive fields).
3. `ImmutableUser`: All fields readonly (cannot be changed after creation).
4. `NewUserInput`: Remove `id` and `createdAt`, keep everything else required.

For each type, create one example object that satisfies it and log one property.

## ANSWER HERE

```typescript
interface User {
  id: string;
  username: string;
  email: string;
  passwordHash: string;
  createdAt: Date;
}

// Write your four derived types and example objects here:


```
