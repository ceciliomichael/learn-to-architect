# Module 06 Exercise: Utility Types & Type Manipulation

Write your solutions inside the **ANSWER HERE** code blocks below.

---

### Challenge 1: Practical Utility Types (`Partial`, `Pick`, `Omit`, `Readonly`)
Given the base interface:
```typescript
interface UserProfile {
  id: string;
  username: string;
  email: string;
  passwordHash: string;
  avatarUrl?: string;
  createdAt: Date;
}
```
Create the following type aliases using TypeScript's built-in utility types:
1. `ProfileUpdatePayload`: All properties are optional, except `id` which is omitted entirely (`Omit` + `Partial`).
2. `PublicProfile`: Only includes `id`, `username`, and `avatarUrl` (`Pick`).
3. `ImmutableProfile`: The entire profile where no property can ever be reassigned (`Readonly`).

#### ✍️ ANSWER HERE:
```typescript
// Write your utility type aliases here:


```

---

### Challenge 2: `keyof` and Lookup Types
Given the interface:
```typescript
interface AppConfig {
  theme: "light" | "dark";
  maxRetries: number;
  enableDebug: boolean;
}
```
1. Write a generic function called `getConfigValue<K extends keyof AppConfig>(config: AppConfig, key: K): AppConfig[K]` that safely retrieves a configuration value.
2. Call your function to get `maxRetries` and verify that TypeScript infers the return type strictly as `number`. Try passing `"nonExistentKey"` and note the compiler error!

#### ✍️ ANSWER HERE:
```typescript
// Write your getConfigValue function here:


```

---

### Challenge 3: `typeof` Type Context
You have an existing configuration object exported by a 3rd party library without a corresponding TypeScript interface:
```typescript
const defaultDatabaseSettings = {
  host: "localhost",
  port: 5432,
  ssl: true,
  poolSize: 10
};
```
Using the `typeof` operator in a type context, create a type alias called `DatabaseSettings` based directly on `defaultDatabaseSettings`. Then create a variable `customSettings: Partial<DatabaseSettings>` overriding only `port` and `poolSize`.

#### ✍️ ANSWER HERE:
```typescript
// Write your DatabaseSettings type and customSettings variable here:


```
