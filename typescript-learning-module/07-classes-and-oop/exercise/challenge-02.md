# Challenge 02: Inheritance and super

Practice extending classes and calling parent methods.

## Your Tasks

1. Create a class `Vehicle` using parameter property shorthand in the constructor
   - `public make: string`
   - `public model: string`
   - `public year: number`
   - A method `describe(): string` that returns `"YEAR MAKE MODEL"` (e.g. `"2023 Toyota Camry"`).

2. Create a class `ElectricVehicle` that `extends Vehicle` and adds
   - `public batteryRangeKm: number` (parameter property shorthand)
   - Override `describe(): string` to return the parent's describe result plus `" (Electric, RANGE km range)"`.
   - Use `super.describe()` inside the override.

3. Create one `Vehicle` instance and one `ElectricVehicle` instance. Call `.describe()` on both and log the results.

4. In a comment, show what `super("Toyota", "Camry", 2023)` does inside the `ElectricVehicle` constructor.

## ANSWER HERE

```typescript
// Write Vehicle and ElectricVehicle here
```
