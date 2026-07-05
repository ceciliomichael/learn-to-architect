# Question 01 Answer: Access Modifiers at Runtime

## Executive Summary & Conceptual Overview
A fundamental concept for TypeScript developers is that **TypeScript types and access modifiers are purely compile-time annotations**. They exist strictly to guide the developer during writing and compilation. Once the TypeScript compiler (`tsc`) transpiles your code into standard JavaScript, every single interface, type alias, and access modifier (`public`, `private`, `protected`, and `readonly`) is completely erased.

Consequently, marking a property `private` in TypeScript prevents external access during development, but it provides **zero runtime data security** in the executed JavaScript bundle.

## Detailed Answers to Quiz Questions

### 1. What does TypeScript's `private` keyword do at compile time?
At compile time, `private` instructs the TypeScript compiler to restrict visibility of the property or method strictly to the body of the class declaring it. If any external code (or even a child subclass extending the parent) attempts to read or assign `account.balance`, the compiler aborts the build with a type error: `Property 'balance' is private and only accessible within class 'BankAccount'`.

### 2. What happens to `private` at runtime in compiled JavaScript?
After compilation, `private` disappears entirely. In the emitted JavaScript code, the property becomes a standard object property. Any runtime JavaScript code executing in Node.js or a browser can freely inspect, read, or modify `account.balance` without restriction.

#### Compile-Time TypeScript Code vs. Emitted Runtime JavaScript
```typescript
// 1. What you write in TypeScript:
export class BankAccount {
  private balance: number;
  constructor(initial: number) {
    this.balance = initial;
  }
}

// 2. What TypeScript emits as JavaScript (after compilation):
export class BankAccount {
  constructor(initial) {
    this.balance = initial; // Notice: 'private' is completely gone!
  }
}

// 3. What an external attacker or script can do at runtime:
const account = new BankAccount(1000);
console.log(account.balance); // Works perfectly at runtime! Outputs: 1000
account.balance = 0;          // Direct modification succeeds at runtime!
```

### 3. Syntax for True, Unbreakable Runtime Privacy
If your application requires genuine cryptographic runtime data privacy (such as storing authentication tokens, encryption keys, or financial balances in browser memory), you must use the ECMAScript **Hash-Prefixed Private Field (`#`)** syntax.

```typescript
export class SecureBankAccount {
  // Hash prefix creates a real JavaScript private field enforced by the JS engine
  #balance: number;

  constructor(initial: number) {
    this.#balance = initial;
  }

  public getBalance(): number {
    return this.#balance;
  }
}

const secureAcc = new SecureBankAccount(5000);
console.log(secureAcc.getBalance()); // Outputs: 5000

// ATTEMPTING EXTERNAL ACCESS:
// console.log(secureAcc.#balance);
// SyntaxError: Private field '#balance' must be declared in an enclosing class
```

## Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Type / Nature | Architectural Role & Meaning |
| :--- | :--- | :--- |
| `private` | TS Compile-Time Modifier | Restricts visibility during compilation only. Erased during JavaScript output generation. |
| `#field` | ECMAScript Private Field | Built-in JavaScript language feature. Enforces strict memory privacy directly inside the JavaScript runtime engine (V8, SpiderMonkey). |
| `tsc` | Compiler CLI | The TypeScript compiler command line interface responsible for type checking and erasing TS annotations into JS. |
| `SyntaxError` | Runtime JS Error | Thrown by the JavaScript engine itself when code outside a class attempts to access a `#`-prefixed field. |

## Architectural Trade-offs: `private` vs. `#field`

Why would an engineer choose TypeScript's `private` over ECMAScript `#field` if `#field` is more secure?
* **Performance & Memory Overhead**: In older JavaScript target environments (ES2015/ES6), transpiling `#field` requires generating WeakMap polyfills to simulate privacy, which increases memory usage and slows down property instantiation. TypeScript's `private` has zero runtime overhead because it compiles to plain properties.
* **Debugging Convenience**: During local development and unit testing, senior engineers often prefer TypeScript's `private` because they can inspect object states in console debuggers without being blocked by runtime engine privacy restrictions.
* **Rule of Thumb**: Use TypeScript `private` for general architectural encapsulation and team boundary enforcement. Use `#field` strictly for highly sensitive secrets (API keys, passwords, cryptographic tokens) that must be shielded from third-party scripts or browser console inspection.
