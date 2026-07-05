# Question 04: Function Inspection and the typeof Context

When integrating third-party libraries or legacy codebases, functions are often exported without accompanying interface definitions for their parameters or return values. This question tests your ability to inspect function signatures programmatically using `ReturnType<T>`, `Parameters<T>`, and `typeof`.

```typescript
// Imagine this function is imported from a third-party SDK
const initializePaymentGateway = (
  apiKey: string,
  merchantId: string,
  options: { timeoutMs: number; retryCount: number; environment: "sandbox" | "production" }
) => {
  return {
    gatewayId: "GW-7788",
    connectedAt: new Date(),
    status: "READY" as const,
    activeEnvironment: options.environment
  };
};
```

## Questions

1. **Runtime vs Compile-Time `typeof`**:
   - What is the exact difference between using `typeof` in a JavaScript expression (`if (typeof apiKey === "string")`) versus using `typeof` in a TypeScript type alias (`type GatewayFn = typeof initializePaymentGateway;`)?
   - Does `typeof initializePaymentGateway` execute the function or add runtime overhead during JavaScript execution? Explain.
2. **Reverse-Engineering Function Signatures**:
   - What is the exact resolved type of `type GatewayReceipt = ReturnType<typeof initializePaymentGateway>;`? Why is `status` typed as `"READY"` instead of `string`?
   - What is the exact resolved type of `type GatewayInputs = Parameters<typeof initializePaymentGateway>;`? Notice the structure: is it an object, a union, or a tuple?
   - How do you write a type expression to extract strictly the `options` parameter object from `GatewayInputs` by indexing into the tuple?

## ANSWER HERE

> **1. Runtime vs Compile-Time `typeof`:**

> **2. Reverse-Engineering Function Signatures (`ReturnType` and `Parameters`):**
