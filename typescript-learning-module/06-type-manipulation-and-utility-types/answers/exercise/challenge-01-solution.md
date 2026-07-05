# Challenge 01 Solution: Object Shape Transformations and Property Pruning

This document provides the verified production implementation, symbol-by-symbol deconstruction, and architectural trade-off analysis for Challenge 01.

## Complete Verified Code Implementation

```typescript
// Master Blueprint Interface
interface MasterUserRecord {
  id: string;
  username?: string; // Originally optional
  email: string;
  passwordHash: string;
  bankAccountNumber: string; // Sensitive financial data!
  createdAt: Date;
}

// 1. UpdateUserPayload: Make all optional, remove id and createdAt
type UpdateUserPayload = Partial<Omit<MasterUserRecord, "id" | "createdAt">>;

const validUpdate: UpdateUserPayload = {
  email: "new_email@enterprise.com",
  username: "updated_username"
};
// Notice: id and createdAt cannot be included, and all remaining fields are optional!

// 2. CompleteRegistrationUser: Make all required, remove sensitive financial fields
type CompleteRegistrationUser = Required<Omit<MasterUserRecord, "bankAccountNumber">>;

const newRegistration: CompleteRegistrationUser = {
  id: "USR-101",
  username: "alice_developer", // Notice: username is strictly required now!
  email: "alice@enterprise.com",
  passwordHash: "argon2i$v=19$m=4096,t=3,p=1$...",
  createdAt: new Date()
};

// 3. ArchivedUserRecord: Lock all properties against reassignment
type ArchivedUserRecord = Readonly<MasterUserRecord>;

const archivedRecord: ArchivedUserRecord = {
  id: "USR-001",
  username: "legacy_user",
  email: "legacy@oldcompany.com",
  passwordHash: "sha256$...",
  bankAccountNumber: "ROUTING-9988",
  createdAt: new Date("2020-01-01")
};
// archivedRecord.email = "hacked@test.com"; 
// COMPILER ERROR: Cannot assign to 'email' because it is a read-only property.

// 4. PublicDirectoryEntry: Pluck strictly display properties
type PublicDirectoryEntry = Pick<MasterUserRecord, "id" | "username" | "email">;

const profileCard: PublicDirectoryEntry = {
  id: "USR-101",
  username: "alice_developer",
  email: "alice@enterprise.com"
};

// 5. SafeVendorPayload: Prune sensitive internal secrets
type SafeVendorPayload = Omit<MasterUserRecord, "passwordHash" | "bankAccountNumber">;

const vendorPayload: SafeVendorPayload = {
  id: "USR-101",
  username: "alice_developer",
  email: "alice@enterprise.com",
  createdAt: new Date()
};

// 6. UserDirectoryMap: Dictionary mapping user IDs to public cards
type UserDirectoryMap = Record<string, PublicDirectoryEntry>;

const directoryMap: UserDirectoryMap = {
  "USR-101": { id: "USR-101", username: "alice_developer", email: "alice@enterprise.com" },
  "USR-102": { id: "USR-102", username: "bob_engineer", email: "bob@enterprise.com" }
};
```

---

## Symbol-by-Symbol Deconstruction

### 1. `Partial<Omit<MasterUserRecord, "id" | "createdAt">>`
* `Partial< ... >`: The built-in type transformer that iterates over every property in the enclosed type and attaches the optional modifier (`?`).
* `Omit< ... >`: The utility engine that copies an existing interface while stripping away specified keys.
* `MasterUserRecord`: The target domain model being transformed.
* `,`: Separates the target interface from the union of keys to remove.
* `"id" | "createdAt"`: A literal string union specifying the exact property names to prune. The pipe (`|`) represents a logical union (both keys are removed).
* **Order of Operations**: TypeScript evaluates from the inside out. First, `Omit` removes `id` and `createdAt`, resulting in a 4-property interface. Then, `Partial` wraps that result, making `username`, `email`, `passwordHash`, and `bankAccountNumber` optional.

### 2. `Required<Omit<MasterUserRecord, "bankAccountNumber">>`
* `Required< ... >`: The built-in transformer that strips away all optional question marks (`?`) from property definitions.
* When applied to our stripped interface, `username?: string` is transformed into `username: string`. Any object attempting to satisfy this type without providing a `username` will be rejected by the compiler.

### 3. `Record<string, PublicDirectoryEntry>`
* `Record<K, V>`: A built-in generic utility that constructs an object dictionary signature.
* `string`: The key constraint `K`. It dictates that property keys in this dictionary must be valid strings.
* `PublicDirectoryEntry`: The value constraint `V`. It enforces that every stored value must conform strictly to the public profile shape.

---

## Architectural Trade-Offs & Best Practices

### Why Deriving Types Beats Manual Duplication
If an enterprise application maintains separate, manually written interfaces for `User`, `UpdateUser`, `PublicUser`, and `ArchivedUser`, adding a new field (such as `isEmailVerified: boolean`) to the database schema requires manually updating four different files. This pattern is prone to human error and type drift. By deriving shapes programmatically using `Pick`, `Omit`, `Partial`, and `Required`, a change to `MasterUserRecord` automatically propagates across the entire application with 100% precision.

### Why `Pick` is Preferred Over `Omit` for Public Views
When defining public-facing data views (like `PublicDirectoryEntry`), senior architects strictly prefer `Pick` over `Omit`. If you use `Omit<MasterUserRecord, "passwordHash" | "bankAccountNumber">`, and a backend engineer later adds a new sensitive field (such as `socialSecurityNumber`) to `MasterUserRecord`, that sensitive field will automatically leak into your public type! Using `Pick<MasterUserRecord, "id" | "username" | "email">` acts as an architectural allow-list: new database columns are excluded by default until explicitly whitelisted.

### Runtime vs Compile-Time Memory Models
It is critical to remember that TypeScript utility types operate exclusively at compile time. When `ArchivedUserRecord` applies `Readonly<T>`, the TypeScript compiler prevents developers from writing assignment statements in code. However, once transpiled to JavaScript, `Readonly<T>` is completely erased. It does not invoke `Object.freeze()` or alter object descriptors in JavaScript runtime memory. If an immutable object is passed to an external, untyped JavaScript library, that library can still mutate the object at runtime without restriction.
