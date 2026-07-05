# Challenge 01: Object Shape Transformations and Property Pruning

Practice deriving multiple domain models from a single master interface without duplicating code. This challenge tests your mastery of built-in Utility Types: `Partial`, `Required`, `Readonly`, `Pick`, `Omit`, and `Record`.

## Master Blueprint Interface

```typescript
interface MasterUserRecord {
  id: string;
  username?: string; // Originally optional
  email: string;
  passwordHash: string;
  bankAccountNumber: string; // Sensitive financial data!
  createdAt: Date;
}
```

## Your Tasks

Using only TypeScript's built-in utility types (do not manually re-type property names or types), create the following six derived type aliases:

1. `UpdateUserPayload`: Convert every property into an optional property, but remove `id` and `createdAt` entirely so they can never be modified during a database PATCH request.
2. `CompleteRegistrationUser`: Convert every property into a strictly required property (stripping away optional modifiers from fields like `username`), while removing sensitive financial fields like `bankAccountNumber`.
3. `ArchivedUserRecord`: Lock every property in the master record against reassignment so that historical records cannot be modified after archiving.
4. `PublicDirectoryEntry`: Pluck strictly the `id`, `username`, and `email` properties for display on a public profile card.
5. `SafeVendorPayload`: Remove sensitive internal secrets (`passwordHash` and `bankAccountNumber`), keeping all other properties intact for external IT integrations.
6. `UserDirectoryMap`: Use `Record` to construct a dictionary object mapping user ID strings (`string`) to `PublicDirectoryEntry` objects.

For each type alias, create one example valid object that satisfies the type contract, and write a comment explaining why TypeScript accepts it.

## ANSWER HERE

```typescript
interface MasterUserRecord {
  id: string;
  username?: string;
  email: string;
  passwordHash: string;
  bankAccountNumber: string;
  createdAt: Date;
}

// 1. UpdateUserPayload


// 2. CompleteRegistrationUser


// 3. ArchivedUserRecord


// 4. PublicDirectoryEntry


// 5. SafeVendorPayload


// 6. UserDirectoryMap


```
