# Answer  -  Question 01: Type Erasure & Boundary Vulnerability

## 1. Why it compiles cleanly under `strict: true`
The code compiles because the `as UserData` type assertion tells the TypeScript compiler: *"Stop verifying this variable; I guarantee `reqBody` conforms to the `UserData` interface."* The compiler accepts this directive and assumes `user.isAdmin` exists and is a boolean.

## 2. Runtime impact of both payloads
- **Payload `{ id: "hacker-1" }` (omitting `isAdmin`)**: At runtime, `user.isAdmin` evaluates to `undefined`. Since `undefined` is falsy in JavaScript, the `if (user.isAdmin)` check fails, and admin access is denied (safe by accident).
- **Payload `{ id: "hacker-2", isAdmin: "true" }` (string instead of boolean)**: At runtime, non-empty strings (`"true"`) evaluate to truthy in JavaScript `if` conditions! The conditional passes, and `grantAdminAccess("hacker-2")` executes, creating a catastrophic privilege escalation vulnerability.

## 3. Why `as` fails to protect the system
Type assertions are completely stripped away during compilation (`tsc`). They do not generate runtime validation code or type casting checks. At runtime, `user` is just raw JSON.

## 4. Production-Grade Implementation

```typescript
interface UserData {
  id: string;
  email: string;
  isAdmin: boolean;
}

// Runtime Type Guard
function isUserData(raw: unknown): raw is UserData {
  return (
    typeof raw === "object" &&
    raw !== null &&
    "id" in raw &&
    typeof (raw as Record<string, unknown>).id === "string" &&
    "email" in raw &&
    typeof (raw as Record<string, unknown>).email === "string" &&
    "isAdmin" in raw &&
    typeof (raw as Record<string, unknown>).isAdmin === "boolean"
  );
}

async function handleLogin(reqBody: unknown): Promise<void> {
  if (!isUserData(reqBody)) {
    throw new Error("Invalid request body schema.");
  }
  // Inside this block, TypeScript automatically narrows reqBody to UserData
  if (reqBody.isAdmin === true) {
    grantAdminAccess(reqBody.id);
  }
}
```
