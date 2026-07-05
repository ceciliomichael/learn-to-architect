# Question 04 Answer: `extends` vs `implements`

## Executive Summary & Conceptual Overview
In TypeScript Object-Oriented design, `extends` and `implements` represent two fundamentally different architectural relationships:
* **`extends` (Class Inheritance)** establishes an **"is-a"** relationship between a derived child class and a parent base class. It inherits physical implementations, properties, methods, and prototype chains at runtime.
* **`implements` (Interface Adoption)** establishes a **"behaves-as"** structural contract. It is purely a compile-time check ensuring that a class publicly contains every property and method signature defined in the interface, without inheriting any runtime code or default logic.

## Detailed Answers to Quiz Questions

### 1. What is the difference between `extends` and `implements`?

| Dimension | `extends` (Class Inheritance) | `implements` (Interface Adoption) |
| :--- | :--- | :--- |
| **Runtime Presence** | Emits real prototype inheritance chains in compiled JavaScript. | Erased completely during JavaScript compilation; zero runtime footprint. |
| **Code Reuse** | Subclasses inherit implemented methods, constructors, and fields from the parent. | Zero code reuse; the implementing class must write 100% of the method bodies from scratch. |
| **Access Modifiers** | Subclasses inherit `public` and `protected` members. | Enforces strictly `public` members; interfaces cannot mandate private or protected fields. |
| **Relationship** | Hierarchical specialization (e.g., `Manager extends Employee`). | Capability certification (e.g., `Document implements Printable`). |

### 2. Why can a class implement multiple interfaces but only extend a single class?
TypeScript and JavaScript strictly enforce **Single Inheritance** for classes (`class Child extends Parent`). A class cannot extend two classes simultaneously (`class Child extends A, B` is illegal). However, a class can implement **Multiple Interfaces** (`class Child implements A, B, C`).

#### The Reason: Preventing the "Diamond Problem"
In programming languages that allow multiple class inheritance (like C++), if Class B and Class C both inherit from Class A, and both override a method called `execute()`, what happens when Class D inherits from both Class B and Class C? When calling `d.execute()`, the runtime cannot deterministically decide whether to execute Class B's version or Class C's version! This ambiguity is known as the **Diamond Problem**.

JavaScript avoids this problem entirely by restricting prototype chains to a single linear path: an object has exactly one prototype reference (`__proto__`). 

Conversely, **interfaces contain zero implementation logic**. If a class implements three interfaces (`implements Printable, Serializable, Loggable`), and all three interfaces happen to define a signature `reset(): void`, there is no conflict! The class simply writes one single concrete `reset()` method body that satisfies all three contracts simultaneously.

## Complete Enterprise Code Example

```typescript
// 1. Multiple Structural Interfaces (Zero implementation, purely compile-time contracts)
export interface Loggable {
  logLevel: string;
  log(message: string): void;
}

export interface Serializable {
  serialize(): string;
}

// 2. Single Base Class (Physical runtime implementation)
export class BaseEntity {
  constructor(public readonly id: string, public createdAt: Date = new Date()) {}

  public getEntityMeta(): string {
    return `Entity[ID=${this.id}, Created=${this.createdAt.toISOString()}]`;
  }
}

// 3. Derived Class: Extends EXACTLY ONE base class, but implements MULTIPLE interfaces!
export class UserAccount extends BaseEntity implements Loggable, Serializable {
  public logLevel: string = "INFO";

  constructor(id: string, public username: string) {
    // Must invoke base constructor first:
    super(id);
  }

  // Satisfying the Loggable interface contract:
  public log(message: string): void {
    console.log(`[${this.logLevel}] User (${this.username}): ${message}`);
  }

  // Satisfying the Serializable interface contract:
  public serialize(): string {
    return JSON.stringify({ id: this.id, username: this.username, created: this.createdAt });
  }
}

// Runtime Execution & Verification
const user = new UserAccount("USR-882", "alice_smith");
console.log(user.getEntityMeta()); // Inherited from BaseEntity via 'extends'
user.log("User logged in successfully."); // Implemented from Loggable
console.log("Serialized Payload:", user.serialize()); // Implemented from Serializable
```

## Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Type / Nature | Architectural Role & Meaning |
| :--- | :--- | :--- |
| `extends` | Single Inheritance | Establishes linear prototype inheritance. Links child prototype to parent prototype. |
| `implements` | Multiple Adoption | Enforces structural type compliance across one or more comma-separated interface contracts. |
| `__proto__` | JS Runtime Pointer | The internal JavaScript engine reference linking an object instance to its parent prototype in memory. |
| `JSON.stringify` | Standard JS API | Converts a JavaScript object or value into a JSON string representation. |
