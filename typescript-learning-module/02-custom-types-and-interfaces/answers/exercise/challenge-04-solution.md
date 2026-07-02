# Challenge 04: Solution

```typescript
type UserId = string | number;

// 1. Start with a string value
let currentId: UserId = "user-123";

if (typeof currentId === "string") {
  console.log(currentId.toUpperCase()); // Outputs: "USER-123"
}

// 2. Change the value to a number
currentId = 404;

if (typeof currentId === "number") {
  console.log("Numeric ID: " + currentId); // Outputs: "Numeric ID: 404"
}
```
