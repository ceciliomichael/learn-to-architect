# Challenge 02: Union Transformations and Function Inspection

Practice filtering complex union types and reverse-engineering function signatures without rewriting code. This challenge tests your mastery of `Exclude`, `Extract`, `NonNullable`, `ReturnType`, and `Parameters`.

## Starting Definitions

```typescript
// Part 1: Union Types
type AllStatusCodes = "IDLE" | "LOADING" | "SUCCESS" | "ERROR" | "TIMEOUT" | null | undefined;
type DatabaseLookupResult = { id: string; username: string; email: string } | null | undefined;

// Part 2: Third-Party Function (Imagine this is imported from an external library without exported types)
function executeFinancialTransaction(
  senderId: string,
  recipientId: string,
  transferAmount: number,
  currencyCode: "USD" | "EUR" | "GBP",
  isUrgent?: boolean
) {
  return {
    transactionId: "TX-889900",
    processedAt: new Date(),
    status: "SETTLED" as const,
    feeCharged: transferAmount * 0.01
  };
}
```

## Your Tasks

**Part 1: Union Filtering and ORM Safety**
1. Create a type alias `ActiveStates` using `Exclude` to remove `"ERROR"`, `"TIMEOUT"`, `null`, and `undefined` from `AllStatusCodes`.
2. Create a type alias `FailureStates` using `Extract` to isolate strictly `"ERROR"` and `"TIMEOUT"` from `AllStatusCodes`.
3. Create a type alias `GuaranteedUser` using `NonNullable` to strip away `null` and `undefined` from `DatabaseLookupResult`. This mirrors how senior architects clean ORM query results before passing data to UI components.

**Part 2: Reverse-Engineering Function Signatures**
4. Create a type alias `TransactionReceipt` using `ReturnType<typeof executeFinancialTransaction>` to capture the exact return shape of the financial function.
5. Create a type alias `TransactionArgs` using `Parameters<typeof executeFinancialTransaction>` to extract all function inputs as a tuple type.
6. Create a type alias `SupportedCurrency` by indexing directly into the `TransactionArgs` tuple (at index `3`) to isolate the `"USD" | "EUR" | "GBP"` currency union!

For every task, write out the type definition and add a comment demonstrating what the resolved type looks like in memory.

## ANSWER HERE

```typescript
// Part 1: Union Types
type AllStatusCodes = "IDLE" | "LOADING" | "SUCCESS" | "ERROR" | "TIMEOUT" | null | undefined;
type DatabaseLookupResult = { id: string; username: string; email: string } | null | undefined;

// Write ActiveStates, FailureStates, and GuaranteedUser here:



// Part 2: Third-Party Function
function executeFinancialTransaction(
  senderId: string,
  recipientId: string,
  transferAmount: number,
  currencyCode: "USD" | "EUR" | "GBP",
  isUrgent?: boolean
) {
  return {
    transactionId: "TX-889900",
    processedAt: new Date(),
    status: "SETTLED" as const,
    feeCharged: transferAmount * 0.01
  };
}

// Write TransactionReceipt, TransactionArgs, and SupportedCurrency here:



```
