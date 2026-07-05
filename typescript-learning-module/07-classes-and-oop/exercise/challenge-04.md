# Challenge 04: Getters, Setters, and Static Members

Practice encapsulating internal state with validation accessors and building class-level utilities using static members.

## Your Tasks

1. Create a class `TemperatureSensor` with:
   - A private property `_celsiusTemp: number` initialized to `20`.
   - A public getter `temperature` that logs `"[LOG]: Reading sensor temperature."` and returns `_celsiusTemp`.
   - A public setter `temperature(newTemp: number)` that validates whether `newTemp` is between `-50` and `100`.
     - If `newTemp` is valid, assign it to `_celsiusTemp` and log `"[LOG]: Temperature adjusted to NEW_TEMP°C."`.
     - If `newTemp` is invalid (less than `-50` or greater than `100`), log an error message `"[ERROR]: Temperature out of safe operating range!"` and do not modify `_celsiusTemp`.

2. Create a class `SensorRegistry` with:
   - A private static array `private static activeSensors: string[] = [];` that stores sensor ID strings.
   - A public static method `registerSensor(sensorId: string): void` that pushes `sensorId` into the `activeSensors` array and logs `"[REGISTRY]: Sensor SENSOR_ID registered."`.
   - A public static method `getActiveCount(): number` that returns the length of the `activeSensors` array.

3. Execution and Testing:
   - Create an instance of `TemperatureSensor`.
   - Read the initial temperature using the getter.
   - Attempt to set a valid temperature of `25`. Verify that it succeeds.
   - Attempt to set an invalid temperature of `150`. Verify that the error is logged and the temperature remains `25`.
   - Call `SensorRegistry.registerSensor("SENSOR-ALPHA")` and `SensorRegistry.registerSensor("SENSOR-BETA")` directly on the class factory without using `new`.
   - Log the total count of active sensors using `SensorRegistry.getActiveCount()`.

## ANSWER HERE

```typescript
// Write your TemperatureSensor and SensorRegistry classes here
```
