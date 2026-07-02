# Challenge 04: Solution

```typescript
type UserId = string | number;

// Start session with OAuth string identifier
let sessionId: UserId = "oauth_99";

if (typeof sessionId === "string") {
  console.log(sessionId.toUpperCase()); // Outputs: "OAUTH_99"
}

// Transition to legacy numeric identifier
sessionId = 404;

if (typeof sessionId === "number") {
  console.log("Legacy ID: " + sessionId); // Outputs: "Legacy ID: 404"
}
```
