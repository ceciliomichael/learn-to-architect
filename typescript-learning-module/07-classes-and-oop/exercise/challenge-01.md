# Challenge 01: Build a Secure Bank Account

Practice access modifiers and the class structure.

## Your Tasks

Create a class `BankAccount` with:
- `readonly accountId: string`  -  set once in the constructor, never changeable.
- `private balance: number`  -  nobody outside the class can read or write it directly.

Public methods:
- `deposit(amount: number): void`  -  adds `amount` to balance, but only if `amount > 0`.
- `withdraw(amount: number): boolean`  -  returns `true` and deducts `amount` if `amount > 0` AND the balance has enough. Returns `false` otherwise.
- `getBalance(): number`  -  returns the current balance.

After building the class:
1. Create an instance with an initial balance of 500.
2. Deposit 200. Log the new balance.
3. Try a successful withdrawal of 300. Log whether it succeeded and the new balance.
4. Try a withdrawal of 1000 (more than available). Log whether it succeeded and the balance.
5. Write a commented-out line trying to access `balance` directly and write the error.

## ANSWER HERE

```typescript
// Write your BankAccount class here:


```
