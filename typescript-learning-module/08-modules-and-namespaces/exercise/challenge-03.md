# Challenge 03: Write a Declaration File

A legacy JavaScript file exposes a global object on `window` that your TypeScript code needs to use. Your job is to describe its shape in a `.d.ts` file.

## The JavaScript Global

This JavaScript code (which you cannot modify) exposes
```javascript
window.PaymentGateway = {
  init(merchantId) { /* ... */ },
  charge(amount, currency) { /* returns a Promise<boolean> */ },
  getStatus() { /* returns 'ready', 'busy', or 'error' */ }
};
```

## Your Task

Write the content of `payment-gateway.d.ts` that types this global object
- `init(merchantId: string): void`
- `charge(amount: number, currency: string): Promise<boolean>`
- `getStatus(): "ready" | "busy" | "error"`

Declare it as an extension of the global `Window` interface. End the file with `export {}` to make it a module and prevent TypeScript from treating it as a script.

## ANSWER HERE

```typescript
// payment-gateway.d.ts


```
