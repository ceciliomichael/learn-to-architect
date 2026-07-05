# Module 10 Exercise Solutions

Reference modular architecture solutions.

---

### Solution 1: Refactored Codebase

**`types.ts`**
```typescript
export interface User {
  id: string;
  name: string;
  age: number;
}
```

**`validator.ts`**
```typescript
import { User } from "./types";

export function isUserOldEnough(user: User): boolean {
  return user.age >= 18;
}
```

**`userRepository.ts`**
```typescript
import { User } from "./types";

export function saveUser(user: User): void {
  console.log(`[DB]: Saving user ${user.id} to storage...`);
}
```

**`index.ts`**
```typescript
import { User } from "./types";
import { isUserOldEnough } from "./validator";
import { saveUser } from "./userRepository";

export function registerUser(id: string, name: string, age: number): void {
  const user: User = { id, name, age };
  if (!isUserOldEnough(user)) {
    console.error("User validation failed.");
    return;
  }
  saveUser(user);
  console.log("Registration complete.");
}
```
