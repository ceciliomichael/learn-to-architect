# Question 01 Answer

**What `private` does at compile time:**
`private` tells the TypeScript compiler to produce an error any time code outside the class tries to read or write the property. It is a guard that catches accidental access during development.

**What happens at runtime after compilation:**
TypeScript's `private` completely disappears after compilation. The generated JavaScript has no access control at all. The property is a normal JavaScript property on the object. At runtime, any JavaScript code can access `account.balance` directly without restriction.

**The syntax for true runtime privacy:**
The JavaScript `#` prefix creates a real private field that is enforced by the JavaScript engine at runtime, not just by the TypeScript compiler
```typescript
class BankAccount {
  #balance: number;
  constructor(initial: number) { this.#balance = initial; }
  getBalance(): number { return this.#balance; }
}
```
`#balance` cannot be accessed from outside the class even in the compiled JavaScript.
