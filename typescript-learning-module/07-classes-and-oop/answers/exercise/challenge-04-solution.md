# Challenge 04 Solution: Getters, Setters, and Static Members

## Executive Summary & Learning Objectives
This solution demonstrates two crucial OOP features: **Accessors (`get` and `set`)** for intercepting property access with validation logic, and **Static Members (`static`)** for building class-level utilities and registries. In production applications, accessors provide clean, intuitive property syntax while secretly enforcing boundary rules. Static members allow engineers to maintain centralized state and utility methods without allocating unnecessary object instances in memory.

## Complete Production-Ready Code

```typescript
export class TemperatureSensor {
  // Private backing field: Stores the actual raw temperature value in memory
  private _celsiusTemp: number = 20;

  // Getter: Intercepts read access (e.g., console.log(sensor.temperature))
  public get temperature(): number {
    console.log("[LOG]: Reading sensor temperature.");
    return this._celsiusTemp;
  }

  // Setter: Intercepts assignment access (e.g., sensor.temperature = 25)
  public set temperature(newTemp: number) {
    if (newTemp < -50 || newTemp > 100) {
      console.error(`[ERROR]: Temperature (${newTemp}°C) out of safe operating range (-50 to 100°C)!`);
      return; // Reject the invalid assignment!
    }
    this._celsiusTemp = newTemp;
    console.log(`[LOG]: Temperature adjusted to ${newTemp}°C.`);
  }
}

export class SensorRegistry {
  // Private static array: Resides strictly on the class constructor object in memory
  private static activeSensors: string[] = [];

  // Public static method: Callable directly on SensorRegistry without 'new'
  public static registerSensor(sensorId: string): void {
    this.activeSensors.push(sensorId);
    console.log(`[REGISTRY]: Sensor ${sensorId} registered successfully.`);
  }

  public static getActiveCount(): number {
    return this.activeSensors.length;
  }
}

// Runtime Execution & Verification
const sensor = new TemperatureSensor();
console.log("Initial Reading:", sensor.temperature);

// Valid assignment triggers the setter validation logic:
sensor.temperature = 25;
console.log("Updated Reading:", sensor.temperature);

// Invalid assignment is blocked by setter validation:
sensor.temperature = 150;
console.log("Reading after invalid attempt:", sensor.temperature);

// Executing static registry methods directly on the class factory:
SensorRegistry.registerSensor("SENSOR-ALPHA");
SensorRegistry.registerSensor("SENSOR-BETA");
SensorRegistry.registerSensor("SENSOR-GAMMA");

console.log("Total Active Sensors:", SensorRegistry.getActiveCount());

// COMPILER ERROR DEMONSTRATION:
// const reg = new SensorRegistry();
// reg.registerSensor("TEST");
// Error: Property 'registerSensor' is a static member of type 'SensorRegistry'.
```

## Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Type / Nature | Architectural Role & Meaning |
| :--- | :--- | :--- |
| `get` | Accessor Keyword | Defines a getter method that executes automatically whenever calling code reads the property name. Must return a value. |
| `set` | Accessor Keyword | Defines a setter method that executes automatically whenever calling code assigns a value using the `=` operator. |
| `_celsiusTemp` | Backing Field | A private property (conventionally prefixed with an underscore) used to store the actual data manipulated by getters and setters. |
| `static` | Memory Modifier | Attaches the property or method directly to the class constructor function object rather than to instantiated object prototypes. |
| `private static` | Combined Modifier | Creates a class-level variable that is shared across the entire application but cannot be read or modified outside the class body. |
| `SensorRegistry.method` | Static Invocation | Direct invocation syntax for static members. Does not require or allow object instantiation via `new`. |

## Architectural Trade-offs & Design Decisions

### 1. Accessors vs. Explicit Methods (`getTemperature()` / `setTemperature()`)
In languages like Java, developers write explicit methods: `sensor.setTemperature(25)`. TypeScript accessors allow us to expose what looks like a simple public field (`sensor.temperature = 25`). This improves API ergonomics and code readability for client developers. When they assign a value, our setter intercepts the operation to perform range validation (`-50` to `100`), logging, and error handling seamlessly.

### 2. Static Registries vs. Singleton Instances
For `SensorRegistry`, we used static members instead of creating an instance (`new SensorRegistry()`). Because a tracking registry must act as a single source of truth across an entire application, attaching state directly to the class blueprint eliminates memory overhead from multiple instances and prevents state fragmentation across disparate object references.

## Common Pitfalls & Anti-Patterns

* **The Infinite Recursion Trap in Setters**: A common junior mistake is writing `public set temperature(val: number) { this.temperature = val; }`. Inside the setter, assigning to `this.temperature` re-invokes the setter method itself! This causes an infinite loop that crashes the application with a `RangeError: Maximum call stack size exceeded`. Always assign to a private backing field (such as `this._celsiusTemp`).
* **Using `this` for Instance Members in Static Methods**: Inside a `static` method, `this` refers to the class constructor function itself, NOT to an object instance. Attempting to access `this.instanceProperty` inside a static method results in a compiler error.

## Runtime Behavior & Output Verification

Executing this code produces the following output:
```text
[LOG]: Reading sensor temperature.
Initial Reading: 20
[LOG]: Temperature adjusted to 25°C.
[LOG]: Reading sensor temperature.
Updated Reading: 25
[ERROR]: Temperature (150°C) out of safe operating range (-50 to 100°C)!
[LOG]: Reading sensor temperature.
Reading after invalid attempt: 25
[REGISTRY]: Sensor SENSOR-ALPHA registered successfully.
[REGISTRY]: Sensor SENSOR-BETA registered successfully.
[REGISTRY]: Sensor SENSOR-GAMMA registered successfully.
Total Active Sensors: 3
```
This confirms that property interception, validation gates, and class-level static tracking operate flawlessly.
