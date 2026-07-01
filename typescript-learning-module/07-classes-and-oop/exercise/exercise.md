# Module 07 Exercise: Classes, Access Modifiers & Interfaces

Write your code inside the **ANSWER HERE** blocks below.

---

### Challenge 1: Secure Bank Account Class
Build a `BankAccount` class:
1. `private balance: number` (initialized via constructor).
2. `readonly accountId: string`.
3. `public deposit(amount: number): void` that adds positive amounts.
4. `public withdraw(amount: number): boolean` that deducts money only if `balance >= amount`, returning `true` on success and `false` on failure.
5. `public getBalance(): number` to read the private balance safely.

#### ✍️ ANSWER HERE:
```typescript
// Write your BankAccount class here:


```

---

### Challenge 2: Parameter Property Shorthand
Rewrite the following class using TypeScript's parameter property shorthand in the constructor so you don't declare properties or assignments explicitly:

```typescript
class Product {
  public name: string;
  private price: number;
  protected sku: string;

  constructor(name: string, price: number, sku: string) {
    this.name = name;
    this.price = price;
    this.sku = sku;
  }
}
```

#### ✍️ ANSWER HERE:
```typescript
// Rewrite the Product class using shorthand here:


```

---

### Challenge 3: Interfaces & Abstract Classes
1. Create an interface `Logger { log(msg: string): void; }`.
2. Create an abstract class `BaseService implements Logger` with:
   - `abstract log(msg: string): void;`
   - `protected serviceName: string;`
   - A concrete method `execute(): void` that calls `this.log(`Executing ${this.serviceName} service...`)`.
3. Create a child class `AuthService` extending `BaseService` that implements `log(msg)` using `console.log`. Instantiate `AuthService` and call `.execute()`.

#### ✍️ ANSWER HERE:
```typescript
// Write your Logger interface, BaseService, and AuthService here:


```
