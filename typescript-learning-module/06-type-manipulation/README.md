# Module 06: Type Manipulation and Utility Types

As your project grows, you will find yourself creating variations of existing interfaces over and over. TypeScript provides built-in tools to transform and reshape types so you do not have to copy and paste interface definitions. These are called **utility types**.

---

## 1. Why Utility Types Exist

Imagine you have a `User` interface for a database record. You need different shapes of it in different places:
- When creating a new user, the `id` should not be provided yet (the database assigns it).
- When displaying a public profile, the `passwordHash` should never be exposed.
- When updating a user, every field should be optional.

Without utility types, you would have to manually write three separate interfaces, all derived from the original `User`. Utility types let you derive them automatically.

```typescript
interface User {
  id: string;
  username: string;
  email: string;
  passwordHash: string;
  createdAt: Date;
}
```

---

## 2. `Partial<T>`: Make All Properties Optional

`Partial<T>` takes a type `T` and returns a new type where every property is optional. This is useful for update payloads where you only want to provide the fields you are changing:

```typescript
type UserUpdatePayload = Partial<User>;
// Result: { id?: string; username?: string; email?: string; ... }

const update: UserUpdatePayload = { email: "newemail@site.com" }; // Valid.
```

---

## 3. `Required<T>`: Make All Properties Mandatory

The opposite of `Partial`. Every optional property becomes required:

```typescript
interface Config {
  host?: string;
  port?: number;
}

type StrictConfig = Required<Config>;
// Result: { host: string; port: number; }
```

---

## 4. `Readonly<T>`: Prevent All Reassignment

`Readonly<T>` returns a type where every property is marked as `readonly`. No property can be changed after the object is created. This is useful for configuration objects or data fetched from a server that should never be mutated locally:

```typescript
type ImmutableUser = Readonly<User>;

const frozenUser: ImmutableUser = {
  id: "1", username: "alice", email: "a@b.com", passwordHash: "xyz", createdAt: new Date()
};

// frozenUser.email = "other@b.com"; // ERROR! Cannot assign to 'email' because it is read-only.
```

---

## 5. `Pick<T, Keys>`: Select Specific Properties

`Pick<T, Keys>` creates a new type containing only the properties you specify. Use it when you want a smaller, focused version of a larger interface:

```typescript
// Only expose id, username, and email. Keep passwordHash hidden.
type PublicUser = Pick<User, "id" | "username" | "email">;

const profile: PublicUser = {
  id: "1",
  username: "alice",
  email: "alice@example.com"
  // passwordHash would be an error here.
};
```

---

## 6. `Omit<T, Keys>`: Remove Specific Properties

`Omit<T, Keys>` is the opposite of `Pick`. It returns a new type with specific properties removed:

```typescript
// Remove 'id' and 'passwordHash' from the full User type:
type NewUserPayload = Omit<User, "id" | "passwordHash" | "createdAt">;
// Result: { username: string; email: string; }
```

---

## 7. `Record<Keys, Type>`: Build a Key-Value Map Type

`Record<Keys, Type>` constructs an object type where the keys come from a union of literal strings and every value has the same type. It is useful for lookup maps and dictionaries:

```typescript
type UserRole = "admin" | "editor" | "viewer";

type PermissionMap = Record<UserRole, boolean>;
// Exactly equivalent to: { admin: boolean; editor: boolean; viewer: boolean; }

const permissions: PermissionMap = {
  admin: true,
  editor: true,
  viewer: false
};
```

---

## 8. The `keyof` Operator

`keyof` takes an interface or type and produces a union of all its property names as literal string types:

```typescript
interface AppConfig {
  theme: "light" | "dark";
  language: string;
  maxRetries: number;
}

type ConfigKey = keyof AppConfig;
// Resolves to: "theme" | "language" | "maxRetries"
```

This is powerful when combined with generics. You can write a function that accepts any property name of a specific type and guarantees the return type matches:

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const config: AppConfig = { theme: "dark", language: "en", maxRetries: 3 };

let theme = getProperty(config, "theme");       // TypeScript knows this returns "light" | "dark".
let retries = getProperty(config, "maxRetries"); // TypeScript knows this returns number.
// getProperty(config, "invalid");              // ERROR! "invalid" is not a key of AppConfig.
```

The return type `T[K]` is called an **indexed access type**. It looks up what type the property `K` holds inside `T`.

---

## 9. Indexed Access Types (`T["key"]`)

You can look up the type of a specific property using square bracket notation in the type system. This is useful when you want to derive a type from an existing object structure:

```typescript
interface Order {
  id: string;
  customer: {
    name: string;
    address: string;
  };
  total: number;
}

// Extract the type of the 'customer' property:
type Customer = Order["customer"];
// Result: { name: string; address: string; }
```

---

## 10. `typeof` in the Type System

You have already seen `typeof` as a runtime operator that returns a string like `"string"` or `"number"`. TypeScript also uses `typeof` in a different way: inside a type declaration, it extracts the type of an existing variable.

This is especially useful when a third-party library gives you a constant object but no corresponding interface:

```typescript
const defaultConfig = {
  host: "localhost",
  port: 5432,
  ssl: false,
  maxConnections: 10
};

// Extract the type of 'defaultConfig' as an interface:
type DatabaseConfig = typeof defaultConfig;
// Result: { host: string; port: number; ssl: boolean; maxConnections: number; }

// Now you can use it to type other variables:
const customConfig: Partial<DatabaseConfig> = { port: 3306 };
```

---

## 11. Combining Utility Types

You can chain multiple utility types together. This is where they become extremely powerful:

```typescript
// Start with User, remove id and createdAt, then make everything optional:
type UserDraft = Partial<Omit<User, "id" | "createdAt">>;
// Result: { username?: string; email?: string; passwordHash?: string; }
```

This is a common real-world pattern for form validation and API request bodies.

---

## 12. Function Utility Types: `ReturnType<T>` and `Parameters<T>`

Sometimes you want to extract types from existing functions instead of objects. TypeScript provides utility types for this:

### `ReturnType<T>`

Extracts the return type of a function type:

```typescript
function createUser() {
  return { id: "123", username: "alice", role: "admin" };
}

// Extract the return type of the createUser function:
type UserOutput = ReturnType<typeof createUser>;
// Result: { id: string; username: string; role: string; }
```

### `Parameters<T>`

Extracts the parameter types of a function as a tuple:

```typescript
function sendEmail(to: string, subject: string, priority: number): boolean {
  return true;
}

// Extract the parameters as a tuple type:
type EmailArgs = Parameters<typeof sendEmail>;
// Result: [to: string, subject: string, priority: number]

const args: EmailArgs = ["bob@example.com", "Hello", 1];
sendEmail(...args); // Safe and fully typed.
```

---

## 13. Writing Custom Mapped Types

Built-in utilities like `Partial` and `Readonly` are not magic  -  they are built using **mapped types**. A mapped type creates a new object type by iterating over the keys of another type using the `[K in keyof T]` syntax:

```typescript
// Here is how TypeScript's built-in Readonly<T> is written under the hood:
type MyReadonly<T> = {
  readonly [K in keyof T]: T[K];
};

// Here is how Partial<T> is written:
type MyPartial<T> = {
  [K in keyof T]?: T[K];
};
```

You can write your own transformations. For example, a type where every property becomes a `Promise`:

```typescript
type AsyncObject<T> = {
  [K in keyof T]: Promise<T[K]>;
};

interface User {
  name: string;
  age: number;
}

type AsyncUser = AsyncObject<User>;
// Result: { name: Promise<string>; age: Promise<number>; }
```

