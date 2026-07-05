# Question 03 Answer: Union Transformations in ORM Queries

This document provides exhaustive technical answers for Question 03, explaining distributive conditional filtering in unions and ORM nullability sanitization.

---

## 1. Symbol-by-Symbol Filtering Mechanics (`Exclude` vs `Extract`)

### How `Exclude` Evaluates Union Members Under the Hood
When you apply `Exclude<DatabaseQueryOutcome, "CONNECTION_TIMEOUT" | "PERMISSION_DENIED">`, TypeScript does not evaluate the union as a single monolithic block. Instead, it invokes **Distributive Conditional Type** algebra. Under the hood, `Exclude<T, U>` is defined in the compiler as:
```typescript
type CustomExclude<T, U> = T extends U ? never : T;
```
Because `T` is a union type, the conditional check distributes across every individual member of the union:
1. `"SUCCESS" extends "CONNECTION_TIMEOUT" | "PERMISSION_DENIED"` -> False -> Returns `"SUCCESS"`
2. `"RECORD_NOT_FOUND" extends "CONNECTION_TIMEOUT" | "PERMISSION_DENIED"` -> False -> Returns `"RECORD_NOT_FOUND"`
3. `"CONNECTION_TIMEOUT" extends "CONNECTION_TIMEOUT" | "PERMISSION_DENIED"` -> True -> Returns `never`
4. `"PERMISSION_DENIED" extends "CONNECTION_TIMEOUT" | "PERMISSION_DENIED"` -> True -> Returns `never`
5. `null extends "CONNECTION_TIMEOUT" | "PERMISSION_DENIED"` -> False -> Returns `null`
6. `undefined extends "CONNECTION_TIMEOUT" | "PERMISSION_DENIED"` -> False -> Returns `undefined`

The compiler then unions the surviving results together:
```typescript
"SUCCESS" | "RECORD_NOT_FOUND" | never | never | null | undefined
```
In TypeScript union algebra, `never` represents an impossible state and is automatically discarded. The exact resulting union type is:
```typescript
type FilteredOutcome = "SUCCESS" | "RECORD_NOT_FOUND" | null | undefined;
```

### The Exact Difference Between `Exclude` and `Extract`
While `Exclude<T, U>` **removes** members of `T` that are assignable to `U` (a subtraction engine), `Extract<T, U>` **isolates and preserves strictly** members of `T` that are assignable to `U` (an intersection/filter engine). Under the hood, `Extract<T, U>` is defined as:
```typescript
type CustomExtract<T, U> = T extends U ? T : never;
```

If we evaluate `Extract<DatabaseQueryOutcome, "RECORD_NOT_FOUND" | "CONNECTION_TIMEOUT" | "INVALID_KEY">`:
* The compiler tests each member of `DatabaseQueryOutcome` against the target union.
* Notice that `"INVALID_KEY"` exists in our filter argument, but does not exist in `DatabaseQueryOutcome`. The compiler simply ignores it because no member of `T` matches it!
* Only `"RECORD_NOT_FOUND"` and `"CONNECTION_TIMEOUT"` exist in both unions.
* The exact resulting union type is:
```typescript
type ExtractedOutcome = "RECORD_NOT_FOUND" | "CONNECTION_TIMEOUT";
```

---

## 2. ORM Nullability Sanitization (`NonNullable`)

### Why Database Lookups Return Nullable Unions
In production Object-Relational Mappers (such as Prisma, TypeORM, Drizzle, or Knex), database lookup operations like `findUnique()` or `findOne()` query table rows based on criteria like primary keys or unique indices. Because a database table cannot guarantee at compile time that a specific ID exists in storage, the lookup might fail to find a matching row. To represent this runtime reality accurately, ORMs type query results as nullable unions: `UserRecord | null | undefined`.

### Why `NonNullable<UserRecord>` Beats Manual Interface Rewriting
When building frontend UI rendering components or backend domain services that process guaranteed user records, you must strip away nullability. A junior developer might attempt to do this by manually writing a new interface:
```typescript
// Inferior: Manual duplication prone to schema drift
interface CleanUserManual {
  id: string;
  email: string;
  role: "admin" | "user";
}
```
Why using `type CleanUser = NonNullable<UserRecord>` is architecturally superior:
1. **Single Source of Truth**: The ORM schema remains the sole authority for database field definitions.
2. **Zero Maintenance Overhead**: You do not have to manually copy and paste property names, types, or union literals across files.
3. **Elimination of Type Drift**: Imagine a database administrator migrates the database schema, adding a new required column `isEmailVerified: boolean` and updating the `role` union to `"admin" | "user" | "superadmin"`. 
   - If you used `CleanUserManual`, your manual interface will drift out of sync, causing downstream functions to operate on incomplete type contracts without compiler warnings!
   - If you used `NonNullable<UserRecord>`, TypeScript automatically recomputes the clean type from the updated ORM definition! Downstream UI components immediately inherit `isEmailVerified` and the updated `role` union with 100% precision.

### Layered Architecture Pattern
In enterprise applications, use `NonNullable<T>` at the exact boundary between your data access layer and your business logic layer:
```typescript
async function getValidatedUser(userId: string): Promise<NonNullable<UserRecord>> {
  const record: UserRecord = await db.users.findUnique({ where: { id: userId } });
  
  // Runtime boundary check:
  if (!record) {
    throw new Error(`User with ID ${userId} not found in database.`);
  }
  
  // After the null check, TypeScript narrows the variable, and we return the clean type!
  return record;
}
```
