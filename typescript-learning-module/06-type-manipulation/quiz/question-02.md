# Question 02: Pick vs Omit

Both `Pick` and `Omit` create a new type from an existing one. When is each one better?

```typescript
interface Employee {
  id: string;
  name: string;
  email: string;
  salary: number;
  department: string;
  startDate: Date;
}
```

1. You need a type with only `id` and `name`. Write both the `Pick` and `Omit` versions. Which is more concise?
2. You need a type with all fields except `salary`. Write both versions. Which is more concise now?
3. As a general rule, when should you use `Pick` and when should you use `Omit`?

## ANSWER HERE

```typescript
// Only id and name
type WithPick = // ...
type WithOmit = // ...

// Everything except salary
type WithPick2 = // ...
type WithOmit2 = // ...
```

> **General rule:**
