# Challenge 04: Solution

```typescript
type UserId = string | number;

// 1. Declare variable with string value
let currentId: UserId = "user-abc-123";

if (typeof currentId === "string") {
  console.log(currentId.toUpperCase()); // Outputs: "USER-ABC-123"
}

// 2. Reassign the exact same variable to a number
currentId = 9001;

if (typeof currentId === "number") {
  console.log("Numeric ID: " + currentId); // Outputs: "Numeric ID: 9001"
}
```
