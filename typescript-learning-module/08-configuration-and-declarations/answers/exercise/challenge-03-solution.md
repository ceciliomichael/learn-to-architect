# Challenge 03: Solution

```typescript
// payment-gateway.d.ts

interface PaymentGateway {
  init(merchantId: string): void;
  charge(amount: number, currency: string): Promise<boolean>;
  getStatus(): "ready" | "busy" | "error";
}

declare global {
  interface Window {
    PaymentGateway: PaymentGateway;
  }
}

export {};
```

The `declare global { ... }` block augments the built-in `Window` interface with the new `PaymentGateway` property. The `export {}` at the end is required to make this file a module (preventing all its declarations from leaking into global scope unintentionally). A declaration file contains only type shapes  -  no executable code, no function bodies.
