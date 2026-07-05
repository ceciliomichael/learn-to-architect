# Question 05 Answer: Abstract Classes

## Executive Summary & Conceptual Overview
An **Abstract Class** in TypeScript is a master architectural blueprint that cannot be instantiated directly using the `new` keyword. It exists strictly to be subclassed via `extends`. 

Abstract classes solve a critical enterprise design challenge: they allow architects to provide **reusable, shared concrete method implementations** across a family of subclasses while simultaneously enforcing **mandatory abstract method signatures** that every child subclass must implement individually.

## Detailed Answers to Quiz Questions

### 1. What are abstract classes used for?
Abstract classes are used to model foundational domain concepts that are too generic or incomplete to exist as standalone physical objects in computer memory. They define a common base structure (shared state, constructor initialization, and common utility methods) while declaring specific domain-dependent operations as `abstract`, forcing derived subclasses to provide custom logic.

### 2. Why choose an abstract class over a regular base class or a pure interface?

| Architecture Choice | Can Instantiate? | Can Contain Concrete Logic? | Can Force Child Implementations? | Best Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **Regular Base Class** | Yes (`new Class()`) | Yes (100% concrete) | No (children can inherit without overriding) | Standalone entities that can exist independently or be extended. |
| **Pure Interface** | No (erased in JS) | No (0% concrete) | Yes (100% mandatory signatures) | Defining cross-cutting structural contracts across unrelated hierarchies. |
| **Abstract Class** | No (`new` blocked) | Yes (Hybrid: concrete + abstract) | Yes (for methods marked `abstract`) | Foundational domain models where children share common core logic but require specialized behavior. |

### 3. Real-World Enterprise Analogy
Imagine the **Federal Aviation Administration (FAA)** publishing a master regulation document titled `AbstractCommercialAircraft`. 

You cannot buy a ticket and fly inside a regulation document! You cannot build an airplane called simply "Commercial Aircraft"; that concept is too generic. Therefore, instantiating `new AbstractCommercialAircraft()` is illegal. 

However, the FAA regulation document contains:
* **Concrete Rules (Implemented Methods)**: *"Every commercial aircraft must possess a standardized black box recorder and an emergency radio beacon."* (Shared code automatically inherited by all planes).
* **Abstract Mandates (Abstract Methods)**: *"Every commercial aircraft manufacturer MUST provide a physical engine ignition system (`startEngines()`) and landing gear deployment system (`deployLandingGear()`)."* Because a Boeing 747 jet starts its engines differently than a Bombardier turboprop propeller plane, the FAA document cannot write the exact engine logic; it marks those methods as `abstract`, forcing Boeing and Bombardier to implement their own specialized mechanics!

## Complete Enterprise Code Example

```typescript
// 1. Abstract Base Class: Uninstantiable master blueprint for Database Drivers
export abstract class DatabaseConnector {
  constructor(protected readonly connectionString: string) {}

  // Concrete method: Shared logging utility inherited by ALL database drivers
  public logConnectionAttempt(): void {
    console.log(`[DB LOG]: Attempting connection to ${this.connectionString}...`);
  }

  // Abstract methods: No implementation allowed! Subclasses MUST provide these!
  public abstract connect(): Promise<boolean>;
  public abstract executeQuery(sql: string): Promise<any[]>;
}

// 2. Concrete Subclass: PostgreSQL Driver
export class PostgresConnector extends DatabaseConnector {
  constructor(connectionString: string, private poolSize: number) {
    super(connectionString);
  }

  // Mandatory implementation of abstract connect():
  public async connect(): Promise<boolean> {
    this.logConnectionAttempt(); // Calling inherited concrete method
    console.log(`[POSTGRES]: Initializing connection pool of size ${this.poolSize}. Connected.`);
    return true;
  }

  // Mandatory implementation of abstract executeQuery():
  public async executeQuery(sql: string): Promise<any[]> {
    console.log(`[POSTGRES]: Executing SQL: "${sql}" via pg-native protocol.`);
    return [{ id: 1, status: "SUCCESS" }];
  }
}

// 3. Concrete Subclass: MongoDb Driver
export class MongoDbConnector extends DatabaseConnector {
  public async connect(): Promise<boolean> {
    this.logConnectionAttempt();
    console.log("[MONGODB]: Establishing wire protocol handshake with MongoDB Atlas.");
    return true;
  }

  public async executeQuery(query: string): Promise<any[]> {
    console.log(`[MONGODB]: Translating SQL "${query}" into BSON aggregation pipeline.`);
    return [{ documentId: "507f1f77bcf86cd799439011" }];
  }
}

// Runtime Execution & Verification
async function runDatabaseDemo() {
  const pg = new PostgresConnector("postgres://admin:secret@db.internal:5432", 10);
  await pg.connect();
  await pg.executeQuery("SELECT * FROM users");

  const mongo = new MongoDbConnector("mongodb://srv.cluster.internal:27017");
  await mongo.connect();
  await mongo.executeQuery("SELECT * FROM orders");
}

runDatabaseDemo();

// COMPILER ERROR DEMONSTRATION:
// const genericDb = new DatabaseConnector("mysql://localhost");
// Error: Cannot create an instance of an abstract class.
```

## Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Type / Nature | Architectural Role & Meaning |
| :--- | :--- | :--- |
| `abstract class` | Blueprint Modifier | Prevents direct object instantiation via `new`. Requires subclassing via `extends`. |
| `abstract method` | Contract Modifier | A method signature without a body inside an abstract class. Enforces mandatory implementation in concrete child classes. |
| `Promise<T>` | Asynchronous Type | Represents the eventual completion or failure of an asynchronous operation returning a value of type `T`. |
| `async / await` | JS Concurrency Syntax | Modern syntactic sugar over Promises, allowing asynchronous database I/O operations to read like synchronous linear code. |
