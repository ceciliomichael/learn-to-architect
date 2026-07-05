# Challenge 01 Solution: Secure Bank Account

## Executive Summary & Learning Objectives
This solution demonstrates how to implement strict **Encapsulation** in TypeScript using access modifiers (`readonly`, `private`, and `public`). In financial software, uncontrolled direct property access is a severe security vulnerability. By hiding the internal balance behind private access modifiers and exposing safe transaction methods, we ensure that state mutations only occur after strict boundary validation.

## Complete Production-Ready Code

```typescript
export class BankAccount {
  // Readonly: Can only be assigned during instantiation; immutable thereafter
  readonly accountId: string;
  
  // Private: Completely hidden from external code and child subclasses
  private balance: number;

  constructor(accountId: string, initialBalance: number) {
    this.accountId = accountId;
    this.balance = initialBalance;
  }

  public deposit(amount: number): void {
    if (amount <= 0) {
      console.error(`[ERROR]: Deposit amount ($${amount}) must be greater than zero.`);
      return;
    }
    this.balance = this.balance + amount;
    console.log(`[LOG]: Deposited $${amount}. New balance: $${this.balance}`);
  }

  public withdraw(amount: number): boolean {
    if (amount <= 0) {
      console.error(`[ERROR]: Withdrawal amount ($${amount}) must be greater than zero.`);
      return false;
    }
    if (this.balance < amount) {
      console.warn(`[WARN]: Insufficient funds for withdrawal of $${amount}. Current balance: $${this.balance}`);
      return false;
    }
    this.balance = this.balance - amount;
    console.log(`[LOG]: Withdrew $${amount}. Remaining balance: $${this.balance}`);
    return true;
  }

  public getBalance(): number {
    return this.balance;
  }
}

// Runtime Execution & Verification
const account = new BankAccount("ACC-1001", 500);
console.log("Initial Balance:", account.getBalance());

account.deposit(200);
const successWithdraw = account.withdraw(300);
console.log("Withdrawal of 300 succeeded?", successWithdraw);

const failedWithdraw = account.withdraw(1000);
console.log("Withdrawal of 1000 succeeded?", failedWithdraw);

// COMPILER ERROR DEMONSTRATION:
// account.balance = 999999;
// Error: Property 'balance' is private and only accessible within class 'BankAccount'.
// account.accountId = "ACC-HACKED";
// Error: Cannot assign to 'accountId' because it is a read-only property.
```

## Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Type / Nature | Architectural Role & Meaning |
| :--- | :--- | :--- |
| `readonly` | Modifier | Ensures the property is assigned strictly once inside the constructor and cannot be altered during the remaining lifecycle of the object instance. |
| `private` | Access Modifier | Restricts visibility strictly to the defining class body. Prevents external callers from modifying financial data directly. |
| `public` | Access Modifier | Exposes methods to external callers, forming the official Application Programming Interface (API) of the class. |
| `this` | Reference Keyword | Points to the specific runtime object instance currently executing the method or being constructed in memory. |
| `constructor` | Built-in Method | Automatically invoked upon calling `new BankAccount(...)` to allocate memory and initialize starting state. |
| `void` | Return Type | Indicates that the `deposit` method performs a side effect (mutating internal balance) without returning a value to the caller. |

## Architectural Trade-offs & Design Decisions

### 1. `private` vs. `protected` for Account Balance
We chose `private` over `protected` for the `balance` field. If `balance` were marked `protected`, a future developer could create a subclass (`class VIPAccount extends BankAccount`) and write a custom method that directly alters `this.balance` without passing through the validation checks in `deposit` or `withdraw`. Using `private` guarantees that even child subclasses must abide by the rules established in the base class.

### 2. Explicit Validation Gates
Notice that both `deposit` and `withdraw` begin with guard clauses checking `if (amount <= 0)`. In enterprise systems, failing early and explicitly logging validation errors prevents corrupt states (such as depositing negative amounts, which would effectively act as an unverified withdrawal).

## Common Pitfalls & Anti-Patterns

* **The Direct Mutation Anti-Pattern**: Writing classes where properties are `public balance: number` without getters or validation methods. This strips away all OOP encapsulation benefits.
* **Forgetting `this`**: In TypeScript and JavaScript, accessing `balance` instead of `this.balance` inside a class method looks for a local variable named `balance` in the function scope rather than the object's instance property, causing a compilation or runtime error.

## Runtime Behavior & Output Verification

When compiled and executed, the script produces the exact chronological sequence of logs below:
```text
Initial Balance: 500
[LOG]: Deposited $200. New balance: $700
[LOG]: Withdrew $300. Remaining balance: $400
Withdrawal of 300 succeeded? true
[WARN]: Insufficient funds for withdrawal of $1000. Current balance: $400
Withdrawal of 1000 succeeded? false
```
This confirms that our encapsulation boundaries and financial validation rules function flawlessly.
