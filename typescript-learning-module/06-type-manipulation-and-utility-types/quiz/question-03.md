# Question 03: Union Transformations in ORM Queries

In production enterprise applications, database Object-Relational Mappers (ORMs) like Prisma, TypeORM, or Drizzle frequently return union types representing potential query outcomes or null states. This question tests how to filter union types using `Exclude`, `Extract`, and `NonNullable`.

```typescript
type DatabaseQueryOutcome = "SUCCESS" | "RECORD_NOT_FOUND" | "CONNECTION_TIMEOUT" | "PERMISSION_DENIED" | null | undefined;
type UserRecord = { id: string; email: string; role: "admin" | "user" } | null | undefined;
```

## Questions

1. **Symbol-by-Symbol Filtering Mechanics**:
   - Explain how `Exclude<DatabaseQueryOutcome, "CONNECTION_TIMEOUT" | "PERMISSION_DENIED">` evaluates union members under the hood. What is the exact resulting union type?
   - What is the exact difference between `Exclude` and `Extract`? If you write `Extract<DatabaseQueryOutcome, "RECORD_NOT_FOUND" | "CONNECTION_TIMEOUT" | "INVALID_KEY">`, what is the resulting union?
2. **ORM Nullability Sanitization**:
   - Why do database lookups return `UserRecord | null | undefined`?
   - If you write a frontend component that requires a guaranteed valid user object, why is using `type CleanUser = NonNullable<UserRecord>` superior to manually writing `{ id: string; email: string; role: "admin" | "user" }`?
   - How does `NonNullable<T>` prevent type drift across an enterprise codebase as database schemas evolve?

## ANSWER HERE

> **1. Symbol-by-Symbol Filtering Mechanics (`Exclude` vs `Extract`):**

> **2. ORM Nullability Sanitization (`NonNullable`):**
