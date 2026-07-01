# Challenge 02: Solution

```typescript
class ValidationError extends Error {
  constructor(public field: string, message: string) {
    super(message);
    this.name = "ValidationError";
  }
}

class NotFoundError extends Error {
  constructor(public resourceId: string) {
    super("Resource not found: " + resourceId);
    this.name = "NotFoundError";
  }
}

function getUserProfile(id: string, name: string): { id: string; name: string } {
  if (id.length === 0) {
    throw new ValidationError("id", "User ID cannot be empty.");
  }
  if (name.length < 2) {
    throw new ValidationError("name", "Name must be at least 2 characters.");
  }
  if (id !== "user-001") {
    throw new NotFoundError(id);
  }
  return { id, name };
}

function safeGet(id: string, name: string): void {
  try {
    const profile = getUserProfile(id, name);
    console.log("Found profile:", profile.name);
  } catch (error) {
    if (error instanceof ValidationError) {
      console.log("Validation failed on field '" + error.field + "': " + error.message);
    } else if (error instanceof NotFoundError) {
      console.log("Not found:", error.resourceId);
    } else if (error instanceof Error) {
      console.log("Unknown error:", error.message);
    }
  }
}

safeGet("",        "Alice"); // Validation: id
safeGet("user-1",  "A");     // Validation: name
safeGet("user-999","Alice"); // Not found
safeGet("user-001","Alice"); // Success
```
