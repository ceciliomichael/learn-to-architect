# Challenge 02: Solution

```typescript
class Vehicle {
  constructor(
    public make: string,
    public model: string,
    public year: number
  ) {}

  describe(): string {
    return `${this.year} ${this.make} ${this.model}`;
  }
}

class ElectricVehicle extends Vehicle {
  constructor(
    make: string,
    model: string,
    year: number,
    public batteryRangeKm: number
  ) {
    // super() calls the Vehicle constructor and initializes make, model, year:
    super(make, model, year);
  }

  override describe(): string {
    return `${super.describe()} (Electric, ${this.batteryRangeKm}km range)`;
  }
}

const car = new Vehicle("Toyota", "Camry", 2023);
console.log(car.describe()); // "2023 Toyota Camry"

const ev = new ElectricVehicle("Tesla", "Model 3", 2024, 560);
console.log(ev.describe());  // "2024 Tesla Model 3 (Electric, 560km range)"
```
