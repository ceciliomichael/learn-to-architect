# Module 06: Type Manipulation and Utility Types

In previous modules, we learned how to build strict, unbreakable blueprints (Interfaces). But in real-world applications, data requirements shift constantly. A User object looks one way when it is fetched from the database, but it looks slightly different when a user is updating their profile, and different again when displayed on a public page.

If you create a brand new, handcrafted Interface for every tiny variation of a User, your codebase will become a bloated, unmaintainable nightmare. 

This module introduces **Utility Types** and **Type Manipulation**—the built-in tools that allow you to dynamically bend, shape, and transform existing blueprints into new ones, saving you from writing duplicate code!

---

## 1. Why Utility Types Exist

### The Real-World Analogy: The Swiss Army Knife Attachments
Imagine buying an expensive electric drill (your base `User` interface). When you need to drill into concrete, you don't throw away the entire drill and buy a "Concrete Drill". You just snap a concrete drill-bit attachment onto your existing drill.

**Utility Types** are snap-on attachments for your existing Interfaces. They take your base blueprint and instantly modify its behavior—making parts of it optional, locking it down, or hiding specific pieces—without permanently altering the original blueprint.

### The Core Technical Concept
Assume we have a central database blueprint for a User:

```typescript
// The Base Blueprint
interface User {
  id: string;
  username: string;
  email: string;
  passwordHash: string;
}
```
Now imagine building an "Edit Profile" screen. The user might only want to change their `email`, leaving the rest blank. Do we write a whole new `interface EditUser` where everything is optional? No! We use a Utility Type.

---

## 2. `Partial<T>`: Make All Properties Optional

### The Core Technical Concept
`Partial<T>` takes a blueprint and returns a clone where *every single property* has a `?` (optional) tag attached to it. 

```typescript
// Applying the Partial attachment to the User blueprint
type UserUpdatePayload = Partial<User>;

// Resulting Blueprint invisibly looks like this:
// { id?: string; username?: string; email?: string; passwordHash?: string; }

// Now we can pass an object with JUST the email!
const updateData: UserUpdatePayload = { email: "newemail@site.com" }; 
```

### Why Production Codebases Rely on This
When writing backend API endpoints to handle HTTP `PATCH` requests (which partially update database records), clients only send the fields they modified. `Partial<T>` guarantees that the update payload perfectly mirrors the database schema, but allows any combination of missing fields.

---

## 3. `Required<T>`: Make All Properties Mandatory

### The Core Technical Concept
`Required<T>` is the exact opposite of `Partial<T>`. It takes a blueprint that has optional `?` properties and strips the question marks off, forcing every single property to be strictly provided.

```typescript
// Base blueprint with optional settings
interface AppConfig {
  host?: string;
  port?: number;
}

// Stripping the optionals away!
type StrictConfig = Required<AppConfig>;

// const myConfig: StrictConfig = { host: "localhost" }; 
// COMPILER ERROR: Property 'port' is missing!
```

### Why Senior Developers Require This
When an application boots up, it reads a `Partial` configuration file from the user. The system then merges that file with default settings to produce a final `Required<AppConfig>`, guaranteeing that downstream server functions never crash due to a missing port number.

---

## 4. `Readonly<T>`: Prevent All Reassignment

### The Real-World Analogy: The Museum Glass Case
You have a beautiful historical document. To prevent people from writing on it, you place it inside a sealed glass case. People can read it, but they cannot alter it.

### The Core Technical Concept
`Readonly<T>` returns a clone of your blueprint where every single property is locked. You cannot modify the object after it is initially created.

```typescript
type ImmutableUser = Readonly<User>;

const frozenUser: ImmutableUser = {
  id: "1", 
  username: "alice", 
  email: "a@b.com", 
  passwordHash: "xyz"
};

// frozenUser.email = "hacked@b.com"; // COMPILER ERROR: Cannot assign to 'email' because it is a read-only property.
```

### Why Production Codebases Rely on This
In frontend state management tools (like Redux or Zustand), global application state must never be mutated directly (`state.counter++`). Wrapping the state blueprint in `Readonly<T>` forces developers to write pure, immutable update functions, eliminating massive classes of UI rendering bugs.

---

## 5. `Pick<T, Keys>`: Select Specific Properties

### The Core Technical Concept
`Pick<T, Keys>` extracts a few specific properties from a massive blueprint and throws the rest away. 

```typescript
// We Pick only the id and username. We leave behind email and passwordHash!
type PublicUserBadge = Pick<User, "id" | "username">;

const profileBadge: PublicUserBadge = {
  id: "u-123",
  username: "alice"
  // If we try to add 'email' here, the compiler will throw an error!
};
```

### Symbol-by-Symbol Syntax Deconstruction
Let us deconstruct `Pick<User, "id" | "username">`:

* `Pick` -> The built-in Utility Type name.
* `<` -> Opening generic bracket.
* `User` -> The target base blueprint we are modifying.
* `,` -> Argument separator.
* `"id" | "username"` -> A Literal Union of the exact string property keys we want to extract.
* `>` -> Closing generic bracket.

---

## 6. `Omit<T, Keys>`: Remove Specific Properties

### The Core Technical Concept
`Omit<T, Keys>` is the exact opposite of `Pick`. Instead of choosing what to keep, you choose what to throw away in the trash.

```typescript
// We want everything EXCEPT the passwordHash!
type SafeUserPayload = Omit<User, "passwordHash">;

// The resulting blueprint invisibly looks like this:
// { id: string; username: string; email: string; }
```

### Why Senior Developers Require This
When a user submits a registration form, the form payload looks exactly like a `User`, EXCEPT it does not have an `id` yet (because the database generates the ID later). Using `type RegistrationForm = Omit<User, "id">` keeps the form perfectly synchronized with the database schema without throwing errors about a missing ID!

---

## 7. `Record<Keys, Type>`: Build a Key-Value Map

### The Real-World Analogy: The Translation Dictionary
Imagine an English-to-French dictionary. Every single word in the dictionary is a string key (the English word), and every single definition is a string value (the French word). 

### The Core Technical Concept
`Record<Keys, Type>` is a utility that instantly generates a dictionary blueprint without you having to type out every single property. 

```typescript
type UserRole = "admin" | "editor" | "viewer";

// We want an object where every Role is a key, and a boolean is the value
type PermissionMap = Record<UserRole, boolean>;

// The above Record generates exactly this:
// { admin: boolean; editor: boolean; viewer: boolean; }

const permissions: PermissionMap = {
  admin: true,
  editor: true,
  viewer: false
};
```

---

## 8. The `keyof` Operator

### The Core Technical Concept
The `keyof` operator is a magic wand. You wave it over an Interface, and it instantly rips out all the property names and turns them into a Literal Union type!

```typescript
interface AppConfig {
  theme: "light" | "dark";
  language: string;
  maxRetries: number;
}

// Wave the magic wand!
type ConfigKey = keyof AppConfig;

// The resulting type is exactly: "theme" | "language" | "maxRetries"
```

### Why Production Codebases Rely on This
If you write a function that looks up properties dynamically, you want the compiler to catch typos. 
`function getValue(obj: AppConfig, key: keyof AppConfig)` guarantees that nobody can accidentally call `getValue(config, "langauge")` (with a typo), because `"langauge"` is not a valid key of the object!

---

## 9. Indexed Access Types (`T["key"]`)

### The Core Technical Concept
Just like you can access a value inside a real JavaScript object using brackets (`customer["address"]`), you can access a nested *Type* inside a TypeScript Interface using identical bracket notation!

```typescript
interface Order {
  id: string;
  customer: {
    name: string;
    address: string;
  };
}

// We drill into the Order interface and extract the shape of the customer!
type CustomerShape = Order["customer"];

// Resulting type is exactly: { name: string; address: string; }
```

### Why Senior Developers Require This
When fetching massive nested API responses (like GraphQL), you often need to extract deeply nested sub-components (like `ApiResponse["data"]["user"]["settings"]`) to pass into smaller React components, without having to manually rewrite those nested shapes from scratch!

---

## 10. `typeof` in the Type System

### The Core Technical Concept
In Module 01, we saw `typeof` used in running JavaScript to check if a variable was a `"string"`. 
But if you use `typeof` inside a TypeScript Type Annotation, it does something entirely different: it reads a physical JavaScript object and *automatically generates a Blueprint Interface from it!*

```typescript
// This is a physical JavaScript object, NOT a blueprint!
const defaultSettings = {
  host: "localhost",
  port: 5432,
  ssl: false
};

// We tell TypeScript: "Generate a blueprint based on the shape of that object!"
type DatabaseConfig = typeof defaultSettings;

// The resulting type is exactly: { host: string; port: number; ssl: boolean; }
```

---

## 11. Combining Utility Types

Utility types become infinitely powerful because they can be chained together!

```typescript
// 1. Omit the id and passwordHash
// 2. Wrap the result in Partial to make everything optional
type DraftUserForm = Partial<Omit<User, "id" | "passwordHash">>;

// Result: { username?: string; email?: string; }
```

---

## 12. Function Utility Types (`ReturnType` and `Parameters`)

Sometimes you want to extract blueprints from *functions* instead of *objects*.

### `ReturnType<T>`
Extracts whatever type a function spits out.
```typescript
function createUser() {
  return { id: "123", role: "admin" };
}

// Automatically grabs the output shape!
type UserOutput = ReturnType<typeof createUser>;
// Result: { id: string; role: string; }
```

### `Parameters<T>`
Extracts the required inputs of a function and turns them into a Tuple Array.
```typescript
function sendEmail(to: string, subject: string): boolean {
  return true;
}

type EmailArgs = Parameters<typeof sendEmail>;
// Result: [to: string, subject: string]
```

---

## 13. Writing Custom Mapped Types

Built-in utilities like `Partial` and `Readonly` are not magic—they are built using **Mapped Types**. A mapped type acts like a `for` loop that runs over the keys of an interface to build a new one.

```typescript
// This is how Partial<T> is written under the hood by Microsoft!
// English: "For every Key (K) in the blueprint (T), make it Optional (?) and keep its original Type (T[K])."
type MyPartial<T> = {
  [K in keyof T]?: T[K];
};
```

You can write your own custom transformers! For example, changing every property to a `Promise`:

```typescript
type AsyncObject<T> = {
  [K in keyof T]: Promise<T[K]>;
};

type AsyncUser = AsyncObject<User>;
// Result: { id: Promise<string>; username: Promise<string>; ... }
```

---

## 14. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **Confusing Runtime `typeof` with Compile-time `typeof`:** 
   - `if (typeof data === "string")` runs in the live browser (JavaScript).
   - `type Config = typeof myObject` runs ONLY in the compiler (TypeScript) and is erased completely before hitting the browser.
2. **Over-Complex Type Gymnastics:** While chained mapped types are powerful (`Partial<Omit<Record<...>>>`), writing overly intricate nested type manipulations can make compiler error messages completely unreadable for your teammates. Always ask: *"Does this complex type utility make the caller's life easier or harder?"* If it makes errors confusing, just write a plain old interface!
3. **`Record<string, any>` Trap:** Beginners often type dynamic dictionaries as `Record<string, any>`. This destroys type safety! Always use `Record<string, unknown>` so you are forced to inspect the dynamic data before using it!
