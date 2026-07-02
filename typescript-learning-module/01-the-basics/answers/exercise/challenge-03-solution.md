# Challenge 03: Solution - Safe Unknown Input

```typescript
let serverResponse: unknown = "Connection established";

// Checking if it is a string before calling string methods
if (typeof serverResponse === "string") {
  console.log(serverResponse.toUpperCase()); // "CONNECTION ESTABLISHED"
}

// Outside the block, TypeScript blocks direct method calls
// serverResponse.toUpperCase();
// ERROR: Object is of type 'unknown'. You must narrow the type first.

// Updated version with a number case too
serverResponse = 500;

if (typeof serverResponse === "string") {
  console.log(serverResponse.toUpperCase());
} else if (typeof serverResponse === "number") {
  console.log("Error code: " + serverResponse); // "Error code: 500"
}
```
