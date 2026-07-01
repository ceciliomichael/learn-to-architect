# Module 07 Exercise Solutions

Reference implementations for Module 07 exercises.

---

### Solution 1: Secure Bank Account Class

```typescript
class BankAccount {
  constructor(
    readonly accountId: string,
    private balance: number
  ) {}

  public deposit(amount: number): void {
    if (amount > 0) {
      this.balance += amount;
    }
  }

  public withdraw(amount: number): boolean {
    if (amount <= 0 || this.balance < amount) {
      return false;
    }
    this.balance -= amount;
    return true;
  }

  public getBalance(): number {
    return this.balance;
  }
}
```

---

### Solution 2: Parameter Property Shorthand

```typescript
class Product {
  constructor(
    public name: string,
    private price: number,
    protected sku: string
  ) {}
}
```

---

### Solution 3: Interfaces & Abstract Classes

```typescript
interface Logger {
  log(msg: string): void;
}

abstract class BaseService implements Logger {
  constructor(protected serviceName: string) {}

  abstract log(msg: string): void;

  public execute(): void {
    this.log(`Executing ${this.serviceName} service...`);
  }
}

class AuthService extends BaseService {
  constructor() {
    super("Auth");
  }

  public log(msg: string): void {
    console.log(`[${this.serviceName}]: ${msg}`);
  }
}

const auth = new AuthService();
auth.execute(); // Logs: [Auth]: Executing Auth service...
```
