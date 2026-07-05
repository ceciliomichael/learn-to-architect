# Module 11: Error Handling and Type-Safe Boundaries

In every software system, things eventually go wrong. Networks drop, databases crash, third-party APIs return corrupted JSON data, and users input invalid credit card numbers. 

If your application lacks robust error handling, an unexpected exception can crash the entire Node.js server process or freeze the browser tab with a blank white screen.

This module teaches you how to build **Type-Safe Error Handling Boundaries** in TypeScript. We will explore how JavaScript's error class hierarchy operates, why caught exceptions are strictly typed as `unknown`, how to build custom domain error classes, how to implement assertion functions, and how to master the **Result Pattern**—a functional programming technique that handles failures without ever throwing exceptions!

---

## 1. The Error Class Hierarchy

### Let's Take Emergency Medical Triage as an Example
To understand how error hierarchies work without getting lost in jargon, imagine an emergency medical clinic in a city hospital.
* **The General Hospital Admission (Base `Error`):** When a patient arrives, they are admitted into the general hospital system. Every single patient shares standard registration attributes: *a patient ID, a medical history record, and a description of their symptom*.
* **Specialized Triage Units (Subclasses):** Not all medical emergencies are identical! A patient with a broken arm is sent to the **Orthopedic Trauma Unit** (`TypeError`), where doctors apply plaster casts. A patient experiencing heart palpitations is sent to the **Cardiac Intensive Care Unit** (`SyntaxError`), where doctors attach EKG monitors.

In TypeScript and JavaScript, when an exception occurs, the runtime doesn't just throw a generic string! It throws an instantiated object from the built-in **`Error` class hierarchy**. Every error object possesses a standard `.message` string and a `.stack` trace, but specialized subclasses represent specific categories of runtime failures!

### Exploring Native Error Classes
JavaScript provides several built-in error classes that inherit from the master `Error` base class:
1. **`Error` (Base Class):** The master parent class for all runtime exceptions.
2. **`TypeError`:** Thrown when an operand or variable is incompatible with the expected type (e.g., trying to call `.toUpperCase()` on `undefined`).
3. **`SyntaxError`:** Thrown when the runtime encounters broken syntax or invalid data formatting (e.g., calling `JSON.parse("bad json")`).
4. **`RangeError`:** Thrown when a numeric value exceeds legal boundaries (e.g., creating an array with `-1` length).

```typescript
// Constructing and throwing standard native error objects
function divideNumbers(a: number, b: number): number {
  if (b === 0) {
    // We instantiate and throw a descriptive Error object!
    throw new Error("Mathematical Error: Division by zero is illegal.");
  }
  return a / b;
}
```

---

## 2. Why Caught Exceptions Are Typed as `unknown`

### Think of Inspecting an Unlabeled Package at a Security Checkpoint
Imagine operating an airport luggage inspection scanner. When a suspicious package arrives at the inspection table (`the catch block`), you cannot blindly assume that the package is an official hard-shell suitcase! 
Why? Because someone might have placed a cardboard box, a plastic shopping bag, or a loose bowling ball onto the conveyor belt!

In TypeScript, when you write a `try / catch` statement, **the caught exception variable is strictly typed as `unknown` by default (`catch (error: unknown)`)**.

Why doesn't TypeScript type it as `catch (error: Error)`? Because in standard JavaScript, developers are legally allowed to throw *any primitive value or object in memory*!
```javascript
// Plain JavaScript legally permits all of these absurd throws:
throw "Server down!";      // Throwing a raw text string!
throw 404;                 // Throwing a number!
throw { status: "fatal" }; // Throwing a plain object literal!
```
Because TypeScript cannot guarantee what third-party npm libraries or legacy scripts might throw across your network boundaries, it enforces strict safety by typing the error as `unknown`. You are physically prohibited from accessing `error.message` until you first verify its shape!

### How to Narrow Caught Exceptions Safely
To inspect a caught exception, use the **`instanceof`** operator to prove to the compiler that the unknown object is an instance of the `Error` class:

```typescript
try {
  const result = divideNumbers(10, 0);
} catch (error: unknown) {
  // Gate 1: We use instanceof to verify if error is an official Error object!
  if (error instanceof Error) {
    // Inside this block, TypeScript narrows 'error' strictly to Error!
    console.error(`[ERROR]: ${error.message}`);
    console.error(`[STACK TRACE]: ${error.stack}`);
  } 
  // Gate 2: If someone threw a raw text string or number!
  else if (typeof error === "string") {
    console.error(`[STRING ERROR]: ${error}`);
  } 
  // Gate 3: Fallback for arbitrary unknown objects
  else {
    console.error("[UNKNOWN FAILURE]: An unrecognized exception occurred.", error);
  }
}
```

---

## 3. Building Custom Domain Error Classes

### Picture Specialized Departmental Warning Citations
Imagine running a municipal city government. When a citizen violates a rule, the police don't issue a generic blank sheet of paper! 
* If a driver parks in a red zone, they receive a **Parking Citation** containing a specific *License Plate Number* and *Meter ID*.
* If a restaurant fails a kitchen hygiene inspection, they receive a **Health Violation Citation** containing a specific *Sanitation Score* and *Closure Date*.

In enterprise TypeScript applications, throwing generic `new Error("failed")` objects makes programmatic debugging difficult. How does your UI know whether an error occurred because *the user's session expired* versus *the database connection dropped*?

You solve this by creating **Custom Domain Error Classes** that inherit from `Error` and attach specialized error codes and metadata properties!

### Designing an Enterprise Error Hierarchy
Let's build a custom error hierarchy for a financial banking application:

```typescript
// 1. The Master Domain Base Error
abstract class BankingDomainError extends Error {
  // We include an HTTP status code and a unique error code string!
  public abstract readonly errorCode: string;
  public abstract readonly httpStatus: number;

  constructor(message: string) {
    super(message);
    // Essential syntax in TypeScript/JavaScript when extending Error:
    Object.setPrototypeOf(this, new.target.prototype);
  }
}

// 2. Specialized Subclass: Insufficient Funds Failure
class InsufficientFundsError extends BankingDomainError {
  public readonly errorCode = "ERR_INSUFFICIENT_FUNDS";
  public readonly httpStatus = 400;

  constructor(public accountId: string, public attemptedAmount: number, public currentBalance: number) {
    super(`Account ${accountId} has insufficient funds ($${currentBalance}) for withdrawal of $${attemptedAmount}.`);
  }
}

// 3. Specialized Subclass: Account Frozen Security Failure
class AccountFrozenError extends BankingDomainError {
  public readonly errorCode = "ERR_ACCOUNT_FROZEN";
  public readonly httpStatus = 403;

  constructor(public accountId: string, public freezeReason: string) {
    super(`Security Alert: Account ${accountId} is frozen. Reason: ${freezeReason}`);
  }
}

// Using our custom domain errors in an ATM withdrawal engine!
function executeAtmWithdrawal(accountId: string, amount: number, balance: number, isFrozen: boolean): void {
  if (isFrozen) {
    throw new AccountFrozenError(accountId, "Suspected fraudulent activity detected.");
  }
  if (amount > balance) {
    throw new InsufficientFundsError(accountId, amount, balance);
  }
  console.log(`Withdrawal of $${amount} successful.`);
}
```

Now, in our global error-handling middleware, we can use `instanceof` to route responses cleanly:

```typescript
try {
  executeAtmWithdrawal("ACC-99", 500, 100, false);
} catch (error: unknown) {
  if (error instanceof InsufficientFundsError) {
    // TypeScript unlocks our custom properties: attemptedAmount and currentBalance!
    console.log(`[ATM DISPLAY]: Please enter an amount under $${error.currentBalance}.`);
  } else if (error instanceof AccountFrozenError) {
    // TypeScript unlocks freezeReason!
    console.log(`[ATM DISPLAY]: Card retained. ${error.freezeReason}`);
  } else if (error instanceof Error) {
    console.log(`[ATM DISPLAY]: System Error: ${error.message}`);
  }
}
```

---

## 4. Assertion Functions (`asserts condition`)

### Think of an Airport Customs Security Gate
When passengers disembark from an international flight, they must walk through a customs passport checkpoint before entering the baggage claim area. 
* If a passenger presents a valid passport, the security officer opens the gate and the passenger walks through into the terminal.
* If a passenger presents an expired or fake passport, **the security officer halts everything immediately**, sounds an alarm, and detains the passenger! The passenger is physically prevented from ever taking another step into the terminal.

In TypeScript, an **Assertion Function** (created using the **`asserts condition`** return type syntax) acts as that customs security checkpoint. It is a function that checks a boolean condition: if the condition is false, the function violently throws an error; if the condition is true, the function returns normally—and **TypeScript permanently narrows the checked variable in all subsequent lines of code!**

### Writing Custom Assertion Guards
When validating complex database results or network payloads, standard `if` checks can clutter your main business logic. Assertion functions let you extract validation rules into reusable checkpoints:

```typescript
// Notice the special return type: 'asserts condition' instead of 'void'!
function assertIsString(value: unknown, fieldName: string): asserts value is string {
  if (typeof value !== "string") {
    throw new TypeError(`Validation Error: Expected ${fieldName} to be a string, but received ${typeof value}.`);
  }
}

function assertIsDefined<T>(value: T | null | undefined, fieldName: string): asserts value is NonNullable<T> {
  if (value === null || value === undefined) {
    throw new Error(`Validation Error: ${fieldName} is strictly required and cannot be null/undefined.`);
  }
}

// Using our assertion functions in an API handler!
function processUserRegistration(payload: { username?: unknown; age?: unknown }): void {
  // At this point, payload.username is 'unknown'
  assertIsDefined(payload.username, "Username");
  assertIsString(payload.username, "Username");
  
  // MAGIC! Because both assertion gates passed without throwing an error,
  // TypeScript narrows payload.username strictly to 'string' for the rest of the function!
  console.log(`Registering user: ${payload.username.toUpperCase()}`);
}
```

---

## 5. The Result Pattern (Functional Error Handling)

### Imagine Sending a Sealed Bank Courier Pouch vs. Setting Off a Fire Alarm
In traditional Object-Oriented programming, throwing exceptions (`throw new Error(...)`) is like **setting off a building fire alarm**. When an alarm rings, normal conversation stops, people drop what they are doing, and everyone scrambles for the fire exits (`the nearest catch block`). Throwing exceptions is computationally expensive and breaks the normal, linear flow of your program.

In Functional Programming (popularized by languages like Rust, Go, and Elm), engineers use a completely different approach: **The Result Pattern**.
Instead of setting off a fire alarm when a calculation fails, your function simply hands back a **Sealed Courier Pouch (`Result<T, E>`)**. 

When you open the pouch, it contains strictly one of two compartments:
1. **The Success Compartment (`Ok<T>`):** Contains a green tag labeled `ok: true`, and your requested data payload!
2. **The Failure Compartment (`Err<E>`):** Contains a red tag labeled `ok: false`, and an error explanation!

Because the function *never throws an exception*, your program never crashes! You simply inspect the tag on the pouch and handle the outcome linearly.

### Building a Type-Safe Result Monad
We can implement the Result Pattern cleanly in TypeScript using a **Discriminated Union**:

```typescript
// 1. The Success Shape
type Ok<T> = {
  readonly ok: true; // The Discriminator Tag!
  readonly value: T;
};

// 2. The Failure Shape
type Err<E> = {
  readonly ok: false; // The Discriminator Tag!
  readonly error: E;
};

// 3. The Discriminated Union!
type Result<T, E = Error> = Ok<T> | Err<E>;

// Helper constructor functions for clean syntax
function createOk<T>(value: T): Ok<T> {
  return { ok: true, value: value };
}

function createErr<E>(error: E): Err<E> {
  return { ok: false, error: error };
}
```

Now, let's see how an enterprise payment processing engine uses the Result Pattern to handle transactions without ever throwing exceptions:

```typescript
// Our function returns Result<number, string> instead of throwing errors!
function processTransfer(accountBalance: number, transferAmount: number): Result<number, string> {
  if (transferAmount <= 0) {
    // Return an Err pouch!
    return createErr("Transfer amount must be greater than zero.");
  }
  if (transferAmount > accountBalance) {
    // Return an Err pouch!
    return createErr(`Insufficient funds. Balance is $${accountBalance}.`);
  }

  const newBalance: number = accountBalance - transferAmount;
  // Return an Ok pouch!
  return createOk(newBalance);
}

// Executing our transfer cleanly without any try/catch blocks!
function handleUiClick() {
  const transferOutcome = processTransfer(500, 750);

  // We simply check the '.ok' tag! TypeScript narrows the union instantly:
  if (transferOutcome.ok === true) {
    // TypeScript knows transferOutcome is strictly Ok<number>!
    console.log(`[SUCCESS]: Transfer complete! Remaining balance: $${transferOutcome.value}`);
  } else {
    // TypeScript knows transferOutcome is strictly Err<string>!
    console.warn(`[TRANSACTION BLOCKED]: ${transferOutcome.error}`);
  }
}
```

### Why Senior Architects Love the Result Pattern
1. **Explicit Signatures:** When a function signature says `function fetchUser(): Promise<User>`, you have no idea what errors it might throw! But when a signature says `function fetchUser(): Promise<Result<User, DatabaseError | NetworkError>>`, every possible failure mode is explicitly documented in the type system!
2. **Zero Runtime Exceptions:** Because errors are treated as normal return values, your Node.js servers and React UI components are completely immune to unhandled exception crashes.
3. **Linear Control Flow:** Your code reads smoothly from top to bottom without jumping across nested `try / catch` scopes.

---

## 6. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **The Empty Catch Block Trap:** Never write an empty catch block!
   ```typescript
   // TERRIBLE (The Silent Graveyard):
   try {
     await saveOrderToDatabase(order);
   } catch (error) {
     // Empty! If the database crashes, the app silently eats the error!
   }

   // PROFESSIONAL ARCHITECTURE:
   try {
     await saveOrderToDatabase(order);
   } catch (error: unknown) {
     console.error("[CRITICAL]: Failed to save order!", error);
     // Re-throw or notify alerting services (like Sentry or Datadog)
     throw error;
   }
   ```
2. **The `instanceof` Trap Across Realms:** In web browsers, if your application utilizes multiple `<iframe>` windows or Web Workers, each frame has its own independent global `Error` object! An error thrown inside an iframe might fail an `error instanceof Error` check in the parent window! In complex browser multi-frame setups, check property existence (`"message" in error && "stack" in error`) alongside `instanceof`.
3. **Throwing Strings Instead of Error Objects:** Never write `throw "Invalid password"`. Why? Because raw strings do not generate a **Stack Trace**! A stack trace (`error.stack`) records the exact sequence of file names and line numbers that led to the crash. Without a stack trace, debugging production errors is almost impossible. Always throw instantiated Error objects: `throw new Error("Invalid password")`.
