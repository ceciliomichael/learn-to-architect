# Challenge 04: Solution

```typescript
type UserId = string | number;

const stringId: UserId = "user-abc-123";
const numericId: UserId = 9001;

function printId(id: UserId): void {
  if (typeof id === "string") {
    console.log(id.toUpperCase()); // "USER-ABC-123"
  } else {
    console.log("ID: " + id); // "ID: 9001"
  }
}

printId(stringId);  // Outputs: USER-ABC-123
printId(numericId); // Outputs: ID: 9001
```
