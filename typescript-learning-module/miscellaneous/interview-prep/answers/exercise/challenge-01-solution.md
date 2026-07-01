# Solution  -  Challenge 01: The Branded ID Architecture

## Detailed Architectural Explanation

In standard TypeScript, type aliases (`type OrderId = string`) are purely stylistic shortcuts. Because TypeScript uses **structural typing**, any string is assignable to `OrderId`, and any `OrderId` is assignable to `CustomerId`. The compiler only sees `string === string`.

To prevent accidental swaps across domain boundaries, we use **Branded Types** (also known as Opaque Types or Tagged Types). By intersecting a primitive string with a unique object shape containing a unique symbol or string tag, TypeScript treats them as completely separate, incompatible types during compilation. At runtime, the tag is completely erased, leaving zero memory or performance overhead.

---

## Full Production Implementation

```typescript
// 1. Generic Branded Utility Type
export type Brand<K, T> = K & { readonly __brand: T };

// 2. Distinct Branded Domain IDs
export type OrderId = Brand<string, "OrderId">;
export type CustomerId = Brand<string, "CustomerId">;

// 3. Validation Constructors (Runtime Gatekeepers)
export function createOrderId(raw: string): OrderId {
  if (!raw || raw.trim().length === 0) {
    throw new Error("Invalid OrderId: cannot be empty string.");
  }
  return raw as OrderId;
}

export function createCustomerId(raw: string): CustomerId {
  if (!raw || raw.trim().length === 0) {
    throw new Error("Invalid CustomerId: cannot be empty string.");
  }
  return raw as CustomerId;
}

// 4. Domain Processing Function
export function processCustomerOrder(customerId: CustomerId, orderId: OrderId): void {
  console.log(`Processing Order ${orderId} for Customer ${customerId}`);
}

// 5. Demonstration
const custId = createCustomerId("CUST-8821");
const ordId = createOrderId("ORD-5519");

// Valid invocation:
processCustomerOrder(custId, ordId);

// COMPILE ERROR: Argument of type 'Brand<string, "OrderId">' is not assignable to parameter of type 'Brand<string, "CustomerId">'.
// processCustomerOrder(ordId, custId);
```
