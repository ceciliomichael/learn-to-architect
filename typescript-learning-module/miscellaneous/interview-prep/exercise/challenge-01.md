# Challenge 01: The Branded ID Architecture

In large enterprise systems, mixing up UUID strings is a frequent source of data corruption bugs (e.g., passing an `OrderUUID` into a function expecting a `CustomerUUID`).

## Your Tasks

1. Explain in comments why plain TypeScript type aliases (`type OrderId = string; type CustomerId = string;`) do not prevent passing an `OrderId` into a function expecting a `CustomerId`. Reference **structural typing** in your explanation.

2. Implement a generic `Brand<K, T>` utility type that attaches a unique phantom symbol or literal tag to a primitive type without changing its runtime representation.

3. Create two distinct branded types: `OrderId` and `CustomerId`.

4. Write two helper constructor functions: `createOrderId(raw: string): OrderId` and `createCustomerId(raw: string): CustomerId` that validate the string is not empty before returning the casted branded type.

5. Write a function `processCustomerOrder(customerId: CustomerId, orderId: OrderId): void` that logs the IDs.

6. Write code demonstrating that calling `processCustomerOrder` with swapped arguments produces a TypeScript compiler error. Include an `ANSWER HERE` code block.

## ANSWER HERE

```typescript
// Write your detailed architectural explanation and Branded Type implementation here:


```
