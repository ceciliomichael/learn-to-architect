# Question 04  -  Answer: `Record` Resolved Type

## Question Recap

> What does `Record<"admin" | "editor", boolean>` resolve to? Write out the exact equivalent interface.

---

## Answer

### Resolved Type

`Record<"admin" | "editor", boolean>` resolves to an object type where every key in the union `"admin" | "editor"` maps to `boolean`.

### Exact Equivalent Interface

```typescript
interface AdminMap {
  admin: boolean;
  editor: boolean;
}
```

These two declarations are **structurally identical** in TypeScript
```typescript
type AdminMap = Record<"admin" | "editor", boolean>;

// Exactly equivalent to
interface AdminMap {
  admin: boolean;
  editor: boolean;
}
```

### Why `Record` Exists

Writing the interface manually is fine for two keys, but `Record` shines when the key union is large, computed, or reused elsewhere
```typescript
type UserRole = 'admin' | 'editor' | 'viewer' | 'moderator' | 'guest';

// Much more concise than writing a 5-property interface
type PermissionMap = Record<UserRole, boolean>;

const permissions: PermissionMap = {
  admin: true,
  editor: true,
  viewer: false,
  moderator: true,
  guest: false,
};
```

If `UserRole` gains a new member (e.g., `'superAdmin'`), TypeScript will immediately flag any `Record<UserRole, boolean>` object that is missing it  -  automatic exhaustiveness checking.

### `Record` vs. Index Signatures

| | `Record<"a" \| "b", T>` | `{ [key: string]: T }` |
|---|---|---|
| Key constraint | Only `"a"` and `"b"` | Any string |
| Exhaustiveness check | Yes | No |
| Use case | Known, finite key set | Open-ended dictionaries |
