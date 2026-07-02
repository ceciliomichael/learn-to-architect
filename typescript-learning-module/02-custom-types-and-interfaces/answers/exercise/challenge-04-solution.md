# Challenge 04: Solution

```typescript
type UserId = string | number;

const stringId: UserId = "user-abc-123";
const numericId: UserId = 9001;

// Checking the string variable directly
if (typeof stringId === "string") {
  console.log(stringId.toUpperCase()); // Outputs: "USER-ABC-123"
} else {
  console.log("Numeric ID: " + stringId);
}

// Checking the numeric variable directly
if (typeof numericId === "string") {
  console.log(numericId.toUpperCase());
} else {
  console.log("Numeric ID: " + numericId); // Outputs: "Numeric ID: 9001"
}
```
