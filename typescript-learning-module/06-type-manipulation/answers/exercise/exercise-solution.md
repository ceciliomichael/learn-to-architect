# Module 06 Exercise Solutions

Reference implementations for Module 06 exercises.

---

### Solution 1: Practical Utility Types

```typescript
interface UserProfile {
  id: string;
  username: string;
  email: string;
  passwordHash: string;
  avatarUrl?: string;
  createdAt: Date;
}

type ProfileUpdatePayload = Partial<Omit<UserProfile, "id">>;
type PublicProfile = Pick<UserProfile, "id" | "username" | "avatarUrl">;
type ImmutableProfile = Readonly<UserProfile>;
```

---

### Solution 2: `keyof` and Lookup Types

```typescript
interface AppConfig {
  theme: "light" | "dark";
  maxRetries: number;
  enableDebug: boolean;
}

function getConfigValue<K extends keyof AppConfig>(config: AppConfig, key: K): AppConfig[K] {
  return config[key];
}

const config: AppConfig = { theme: "dark", maxRetries: 3, enableDebug: true };
const retries = getConfigValue(config, "maxRetries"); // Inferred as number

// Error: Argument of type '"nonExistentKey"' is not assignable to parameter of type 'keyof AppConfig'.
// getConfigValue(config, "nonExistentKey");
```

---

### Solution 3: `typeof` Type Context

```typescript
const defaultDatabaseSettings = {
  host: "localhost",
  port: 5432,
  ssl: true,
  poolSize: 10
};

type DatabaseSettings = typeof defaultDatabaseSettings;

const customSettings: Partial<DatabaseSettings> = {
  port: 3306,
  poolSize: 50
};
```
