# Question 03: Exhaustiveness Checking & The `never` Bottom Type

In a team code review, a developer writes the following payment reducer:

```typescript
type PaymentAction =
  | { type: "CHARGE"; amount: number }
  | { type: "REFUND"; amount: number };

function reducePayment(action: PaymentAction): string {
  switch (action.type) {
    case "CHARGE":
      return `Charging $${action.amount}`;
    case "REFUND":
      return `Refunding $${action.amount}`;
  }
}
```

Six months later, another developer adds a third action to the union:
```typescript
type PaymentAction =
  | { type: "CHARGE"; amount: number }
  | { type: "REFUND"; amount: number }
  | { type: "DISPUTE"; reason: string };
```

1. Without modifying `reducePayment`, what does `reducePayment({ type: "DISPUTE", reason: "Fraud" })` return at runtime? Does TypeScript produce a compile error if the return type of `reducePayment` was inferred instead of explicitly typed as `: string`?
2. Explain what the **`never` bottom type** is in TypeScript type theory.
3. Show how adding a `default` block assigning `action` to a variable of type `never` guarantees compile-time detection of unhandled union members.

## ANSWER HERE

> **1. Runtime return value and compiler behavior:**

> **2. The `never` bottom type explained:**

```typescript
// 3. The exhaustive switch implementation:

```
