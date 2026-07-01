# Answer  -  Question 03: Exhaustiveness Checking & The `never` Bottom Type

## 1. Runtime Return Value & Compiler Behavior
- **At runtime**: When `reducePayment({ type: "DISPUTE", reason: "Fraud" })` executes, the `switch` statement finds no matching `case`. Execution falls through the entire block and implicitly returns `undefined`.
- **Compiler behavior**: If `reducePayment` has an explicit return annotation `: string`, TypeScript throws a compiler error because `undefined` is not assignable to `string`. However, if the return type was *inferred*, TypeScript silently infers `string | undefined`, hiding the bug until a caller tries to call string methods on `undefined`!

## 2. The `never` Bottom Type Explained
In type set theory, `never` is the **empty set** (the bottom type). It represents a value or state that can never exist. No value can ever be assigned to a variable of type `never` (not even `any`).

## 3. Exhaustive Switch Implementation

```typescript
type PaymentAction =
  | { type: "CHARGE"; amount: number }
  | { type: "REFUND"; amount: number }
  | { type: "DISPUTE"; reason: string };

function reducePayment(action: PaymentAction): string {
  switch (action.type) {
    case "CHARGE":
      return `Charging $${action.amount}`;
    case "REFUND":
      return `Refunding $${action.amount}`;
    case "DISPUTE":
      return `Disputed: ${action.reason}`;
    default:
      // If all union members are handled above, 'action' is narrowed to type 'never'.
      // If a new member is added to PaymentAction later without a case block,
      // TypeScript immediately fails compilation right here:
      // Type '({ type: "NEW_ACTION" })' is not assignable to type 'never'.
      const _exhaustiveCheck: never = action;
      return _exhaustiveCheck;
  }
}
```
