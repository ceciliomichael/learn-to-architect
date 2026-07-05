# Question 06 Answer: Getters, Setters, and Static Members

## Executive Summary & Conceptual Overview
This answer explores two advanced Object-Oriented mechanisms: **Accessors (`get` and `set`)** for intercepting property access, and **Static Members (`static`)** for allocating class-level utilities.

Understanding these features requires examining how JavaScript engines organize memory. Instance members reside on individual object heap allocations and prototypes, whereas static members are attached directly to the class constructor function object in memory.

## Detailed Answers to Quiz Questions

### 1. Architectural Advantage of `get` / `set` Accessors
Why prefer `get temperature()` and `set temperature(val)` over standard methods like `getTemperature()` and `setTemperature(val)` or public fields?
* **Ergonomics & API Simplicity**: Accessors allow client code to interact with an object using natural property assignment syntax (`sensor.temperature = 25`) rather than cumbersome method invocations (`sensor.setTemperature(25)`).
* **Encapsulated Boundary Control**: Unlike public fields (`public temperature: number`), accessors act as invisible interceptors. When an assignment occurs, the setter executes custom validation logic, authorization checks, logging, or UI re-rendering before modifying the private backing field in memory.
* **Refactoring Safety**: If a class starts with a simple public field, converting it later to explicit `getVal()` / `setVal()` methods breaks all consuming client code across the project! Converting a public field into a `get` / `set` accessor pair is 100% backward-compatible; calling syntax remains unchanged.

### 2. Memory Storage of `static` Members and the Behavior of `this`
When you declare a property or method as `static`, where is it stored in memory?
* **Memory Layout**: In JavaScript, a class is syntactically a constructor function object. When you instantiate an object via `new ClassName()`, instance properties (`this.prop`) are allocated in a new heap space, and instance methods reside on `ClassName.prototype`. **Static members are attached directly as properties of the `ClassName` constructor function object itself!** They do not exist on `ClassName.prototype` or inside object instances.

#### Why you CANNOT access `this.instanceProperty` inside a static method:
Inside an instance method, `this` points to the instantiated object on the heap. Inside a `static` method, `this` points strictly to the **Class Constructor Function Object itself (`ClassName`)**, NOT to an instance! Because instance properties are only created when `new ClassName()` runs, trying to read `this.instanceProperty` inside a static method returns `undefined` or throws a compiler error because no object instance exists in that execution context.

### 3. Real-World Enterprise Use Case for Static Members
In enterprise backend architectures, static members are universally used for:
1. **Database Connection Pool Singletons**: You do not want 100 different incoming HTTP request handlers creating 100 separate database connection pool objects! A static class `DatabasePool` maintains a single static array of active socket connections shared across the entire server process.
2. **Environment Configuration Loaders**: A static class `AppConfig` parses environment variables (`.env`) exactly once when the server boots up and stores them in static readonly properties (`AppConfig.API_PORT`, `AppConfig.DB_URI`), allowing any service to read configuration cleanly without instantiating config reader objects.

## Complete Enterprise Code Example

```typescript
// 1. Enterprise Database Pool Manager using Static Members
export class DatabasePoolManager {
  // Static private property: Stored strictly once on the class constructor object
  private static activeConnections: number = 0;
  private static readonly MAX_CONNECTIONS: number = 50;

  // Static method: Callable directly without 'new'
  public static acquireConnection(): boolean {
    if (this.activeConnections >= this.MAX_CONNECTIONS) {
      console.error("[POOL ERROR]: Connection pool exhausted! Max limit reached.");
      return false;
    }
    this.activeConnections++;
    console.log(`[POOL LOG]: Connection acquired. Active: ${this.activeConnections}/${this.MAX_CONNECTIONS}`);
    return true;
  }

  public static releaseConnection(): void {
    if (this.activeConnections > 0) {
      this.activeConnections--;
      console.log(`[POOL LOG]: Connection released. Active: ${this.activeConnections}/${this.MAX_CONNECTIONS}`);
    }
  }

  public static getPoolStatus(): string {
    return `Pool Status: ${this.activeConnections}/${this.MAX_CONNECTIONS} active connections.`;
  }
}

// 2. Domain Entity using Getters and Setters for Validation
export class SecureServerConfig {
  private _port: number = 8080;

  public get port(): number {
    return this._port;
  }

  public set port(newPort: number) {
    if (newPort < 1024 || newPort > 65535) {
      console.error(`[CONFIG ERROR]: Port ${newPort} is invalid. Must be between 1024 and 65535.`);
      return;
    }
    this._port = newPort;
    console.log(`[CONFIG LOG]: Server port updated to ${this._port}.`);
  }
}

// Runtime Execution & Verification
console.log("--- Executing Static Pool Operations ---");
DatabasePoolManager.acquireConnection();
DatabasePoolManager.acquireConnection();
console.log(DatabasePoolManager.getPoolStatus());
DatabasePoolManager.releaseConnection();

console.log("--- Executing Accessor Validation ---");
const server = new SecureServerConfig();
console.log("Default Port:", server.port);
server.port = 3000; // Valid assignment
server.port = 80;   // Invalid assignment (privileged system port blocked by setter)
```

## Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Type / Nature | Architectural Role & Meaning |
| :--- | :--- | :--- |
| `get` | Accessor Keyword | Intercepts property read access. Enables computed returns or logging without method call syntax. |
| `set` | Accessor Keyword | Intercepts property assignment access (`=`). Enables validation gating and side-effect logging. |
| `static` | Class-Level Modifier | Attaches members directly to the class constructor function object rather than instance prototypes. |
| `ClassName.method()` | Direct Invocation | The required syntax for invoking static utilities. Bypasses object instantiation entirely. |
| `this` (in static) | Constructor Pointer | Inside a static method, `this` evaluates to the class constructor function itself (`DatabasePoolManager`). |
