# Question 02 Answer: private vs protected

## Executive Summary & Conceptual Overview
In Object-Oriented architecture, controlling visibility across class boundaries is essential for maintaining encapsulation. While `public` allows universal access, senior engineers must carefully choose between **`private`** and **`protected`** when designing classes intended for inheritance. 

The fundamental rule of thumb is: **`private` restricts access strictly to the declaring class body**, whereas **`protected` extends that visibility to child subclasses** inheriting from the base class via `extends`, while remaining strictly hidden from external calling code.

## Deconstructing the Quiz Scenario

Below is the line-by-line analysis of the commented-out lines in the quiz problem:

```typescript
class Vehicle {
  private engineCode: string = "V8-001";
  protected fuelType: string = "gasoline";
}

class ElectricCar extends Vehicle {
  switchFuel(): void {
    // 1. this.engineCode = "EV-002"; -> BLOCKED
    // 2. this.fuelType = "electric"; -> ALLOWED
  }
}

const car = new Vehicle();
// 3. car.engineCode = "V6-005"; -> BLOCKED
// 4. car.fuelType   = "diesel"; -> BLOCKED
```

### 1. `this.engineCode` in `ElectricCar.switchFuel()`: **BLOCKED**
* **Why**: The property `engineCode` is declared as `private` inside `Vehicle`. In TypeScript, `private` members are completely invisible to derived child classes. Even though `ElectricCar` extends `Vehicle`, it has zero access to `Vehicle`'s private fields.
* **Compiler Error**: `Property 'engineCode' is private and only accessible within class 'Vehicle'.`

### 2. `this.fuelType` in `ElectricCar.switchFuel()`: **ALLOWED**
* **Why**: The property `fuelType` is declared as `protected` inside `Vehicle`. The `protected` modifier explicitly grants read and write access to the declaring class AND any derived subclass inheriting from it (`ElectricCar extends Vehicle`).
* **Result**: The subclass can safely mutate or read `this.fuelType` as part of its specialized behavior.

### 3. `car.engineCode` from outside the class: **BLOCKED**
* **Why**: External code (such as global scripts or other modules holding an instance reference `car`) is strictly forbidden from accessing `private` members.
* **Compiler Error**: `Property 'engineCode' is private and only accessible within class 'Vehicle'.`

### 4. `car.fuelType` from outside the class: **BLOCKED**
* **Why**: This is a common point of confusion for junior developers. While `protected` allows access inside child subclasses, **it does not make the property public to the outside world**. External code holding an instance reference cannot read or assign a protected property.
* **Compiler Error**: `Property 'fuelType' is protected and only accessible within class 'Vehicle' and its subclasses.`

## Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Type / Nature | Architectural Role & Meaning |
| :--- | :--- | :--- |
| `private` | Access Modifier | Visibility tier 1 (Most restrictive). Accessible exclusively within the `{ ... }` body of the exact class declaring it. |
| `protected` | Access Modifier | Visibility tier 2 (Inheritance tier). Accessible within the declaring class body AND within the `{ ... }` body of any derived subclass. |
| `public` | Access Modifier | Visibility tier 3 (Open tier). Accessible from anywhere, including external module scripts holding an instance reference. |
| `extends` | Inheritance Keyword | Links a derived child subclass to a parent base class, inheriting all public and protected members into the child's prototype chain. |

## Architectural Trade-offs: When to Choose `protected` over `private`

When building enterprise software, defaulting everything to `private` is safest for encapsulation, but it can make inheritance rigid. You should choose `protected` over `private` in the following scenarios:

1. **Template Method Design Pattern**: When building an abstract base class or framework class where the parent defines the skeleton of an algorithm, but child subclasses must provide domain-specific data or helper utilities.
2. **Shared Base Service Loggers**: In backend microservices, a base class `BaseService` might declare `protected serviceName: string` and `protected log(msg: string)`. Child services (`AuthService`, `BillingService`) inherit these protected helpers to emit formatted logs without exposing logging internals to external controllers.

#### Enterprise Code Example: Proper `protected` Usage
```typescript
export abstract class BaseRepository<T> {
  // Protected: Subclasses need access to the database table name to construct queries,
  // but external API controllers should NEVER see or change the table name!
  protected constructor(protected readonly tableName: string) {}

  protected logQuery(query: string): void {
    console.log(`[DB LOG - ${this.tableName}]: Executing ${query}`);
  }
}

export class UserRepository extends BaseRepository<{ id: string; name: string }> {
  constructor() {
    super("users_table");
  }

  public findUserById(id: string): void {
    // Subclass safely accesses protected parent methods and properties:
    this.logQuery(`SELECT * FROM ${this.tableName} WHERE id = '${id}'`);
  }
}
```
