# Question 02: private vs protected

What is the difference between `private` and `protected`?

```typescript
class Vehicle {
  private engineCode: string = "V8-001";
  protected fuelType: string = "gasoline";

  start(): void {
    console.log(this.engineCode); // Works here (same class).
    console.log(this.fuelType);   // Works here (same class).
  }
}

class ElectricCar extends Vehicle {
  switchFuel(): void {
    // this.engineCode = "EV-002"; // Does this work?
    // this.fuelType = "electric"; // Does this work?
  }
}

const car = new Vehicle();
// car.engineCode = "V6-005"; // Does this work?
// car.fuelType   = "diesel"; // Does this work?
```

For each commented-out line, say whether it is allowed or blocked and why.

## ANSWER HERE

> **`this.engineCode` in `ElectricCar.switchFuel()`:**

> **`this.fuelType` in `ElectricCar.switchFuel()`:**

> **`car.engineCode` from outside the class:**

> **`car.fuelType` from outside the class:**

> **When would you choose `protected` over `private`?**
