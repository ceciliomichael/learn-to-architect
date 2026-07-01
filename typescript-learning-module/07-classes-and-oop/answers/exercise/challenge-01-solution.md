# Challenge 01: Solution

```typescript
class BankAccount {
  readonly accountId: string;
  private balance: number;

  constructor(accountId: string, initialBalance: number) {
    this.accountId = accountId;
    this.balance = initialBalance;
  }

  deposit(amount: number): void {
    if (amount > 0) {
      this.balance = this.balance + amount;
    }
  }

  withdraw(amount: number): boolean {
    if (amount > 0 && this.balance >= amount) {
      this.balance = this.balance - amount;
      return true;
    }
    return false;
  }

  getBalance(): number {
    return this.balance;
  }
}

const account = new BankAccount("ACC-001", 500);

account.deposit(200);
console.log("After deposit:", account.getBalance()); // 700

const w1 = account.withdraw(300);
console.log("Withdrew 300:", w1, "| Balance:", account.getBalance()); // true | 400

const w2 = account.withdraw(1000);
console.log("Withdrew 1000:", w2, "| Balance:", account.getBalance()); // false | 400

// console.log(account.balance);
// ERROR: Property 'balance' is private and only accessible within class 'BankAccount'.
```
