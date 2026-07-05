# Module 11: Error Handling

In a perfect world, databases never go offline, users never mistype their passwords, and networks never drop connections. In reality, software fails constantly.

A junior developer writes code assuming everything will succeed. A senior engineer writes code assuming everything will eventually fail, and builds safety nets to catch those failures gracefully. This module teaches you how to construct those safety nets using advanced TypeScript error handling.

---

## 1. What is an Error?

### The Real-World Analogy: The Assembly Line Halt Button
Imagine a car factory assembly line. A worker is installing a steering wheel, but they realize the steering wheel is broken. 
If they just ignore it and let the car keep rolling down the line, the customer gets a broken car (a Silent Bug). 
Instead, the worker smashes a big red **Halt Button**. The entire assembly line stops immediately, sirens flash, and a manager comes over to fix the exact problem.

### The Core Technical Concept
In software, smashing the big red Halt Button is called **Throwing an Exception**. 

When a piece of code encounters an impossible situation (like trying to read a file that doesn't exist), it uses the `throw` keyword to smash the Halt Button. 
If no one "catches" the exception, the error bubbles all the way to the top and completely crashes your program, turning the user's screen white.

```typescript
function divide(a: number, b: number): number {
  if (b === 0) {
    // Smashing the Halt Button!
    throw new Error("Cannot divide by zero."); 
  }
  return a / b;
}

// If we run this, the program violently crashes and stops executing forever!
// const result = divide(10, 0); 
```

---

## 2. `try`, `catch`, `finally`

### The Real-World Analogy: The Safety Net
If a trapeze artist falls, they don't smash into the ground (a program crash). They fall into a large safety net (`catch`) where medics check if they are okay, and then the show continues (`finally`).

### The Core Technical Concept
You wrap risky code inside a `try` block. If a Halt Button is smashed anywhere inside the `try` block, the program *does not crash*. Instead, execution instantly teleports into the `catch` block.

```typescript
try {
  // 1. The Trapeze Jump (Risky code)
  console.log("Attempting division...");
  const result = divide(10, 0); 
  
  // This line is NEVER reached because the line above throws!
  console.log("Success! Result:", result);

} catch (error) {
  // 2. The Safety Net
  // If ANY code inside 'try' throws, we teleport here!
  console.log("The operation failed gracefully. No crash!");

} finally {
  // 3. The Cleanup Crew
  // This block runs ALWAYS, regardless of success or failure.
  console.log("Closing resources and moving on.");
}
```

### Why Production Codebases Rely on `finally`
Imagine you open a connection to a Database. You try to write data, but it fails. If you don't close the connection, your server will eventually run out of connections and crash. Putting `db.closeConnection()` inside a `finally` block guarantees that the connection is closed whether the write succeeded or failed!

---

## 3. The `Error` Object

When you smash the Halt Button, you must throw a physical object that describes *why* you smashed it. JavaScript has a built-in `Error` class for this.

```typescript
const myError = new Error("Database timeout");

console.log(myError.message); // "Database timeout"
console.log(myError.name);    // "Error"

// The Stack Trace is a massive string showing exactly which file 
// and line number the error occurred on!
console.log(myError.stack);   
```

---

## 4. Typing the `catch` Variable (The `unknown` Trap)

### The Core Technical Concept
In JavaScript, you are legally allowed to throw *anything*. A malicious developer could literally write `throw "potato"`. 

Because you don't know what was thrown, TypeScript strictly types the variable inside a `catch` block as `unknown`. You are not allowed to blindly read `.message` from it, because a string doesn't have a `.message` property!

You must use the `instanceof` operator to mathematically prove to the compiler that the object is a real Error.

```typescript
try {
  throw new Error("Network offline");
} catch (error) {
  // console.log(error.message); // COMPILER ERROR: Object is of type 'unknown'.

  // We ask the security guard: "Was this object manufactured by the Error class?"
  if (error instanceof Error) {
    // Inside this block, TypeScript allows us to read the message!
    console.log("Failed:", error.message);
  } else {
    // If it was a raw string or number, we handle it here.
    console.log("Someone threw a non-error object!", error);
  }
}
```

---

## 5. Custom Error Classes

### The Core Technical Concept
Throwing a generic `Error` is like a car dashboard having one single "Check Engine" light. It doesn't tell you if the tire is flat or the engine is on fire. 

Professional architectures create specific, custom Error classes by extending the base `Error` blueprint. This allows you to write targeted `catch` blocks!

```typescript
// Custom Blueprint 1
class ValidationError extends Error {
  constructor(public fieldName: string, message: string) {
    super(message); // Call the parent Error constructor
    this.name = "ValidationError";
  }
}

// Custom Blueprint 2
class DatabaseError extends Error {
  constructor(message: string) {
    super(message);
    this.name = "DatabaseError";
  }
}
```

Now, when catching the error, you can inspect exactly *which* type of error was thrown!

```typescript
try {
  // Simulate a failure
  throw new ValidationError("password", "Too short");
} catch (error) {
  
  if (error instanceof ValidationError) {
    // TypeScript knows error.fieldName exists!
    console.log(`UI Error on ${error.fieldName}: ${error.message}`);
  } 
  else if (error instanceof DatabaseError) {
    console.log(`DB Alert: ${error.message}`);
  }
}
```

### Why Senior Developers Require This
In web servers (Express/NestJS), you can write a global error handler that catches all errors. If the error is a `ValidationError`, the server automatically returns a `400 Bad Request` to the user. If the error is a `DatabaseError`, the server automatically returns a `500 Internal Server Error` and pages the DevOps team!

---

## 6. Rethrowing Errors

### The Core Technical Concept
Sometimes a function catches an error, looks at it, realizes it doesn't know how to fix it, and throws it back up into the air for a higher-level function to deal with. This is called **Rethrowing**.

```typescript
async function processPayment(amount: number) {
  try {
    await stripe.charge(amount);
  } catch (error) {
    if (error instanceof StripeCardDeclinedError) {
      console.log("Card declined. Ask user for a new card.");
      return; // Handled safely!
    }
    
    // We don't know what this error is (maybe the Stripe API is down).
    // Throw it back up to the caller!
    throw error; 
  }
}
```

---

## 7. The Result Pattern: Errors as Data

### The Real-World Analogy: The Delivery Report
Instead of a mailman screaming in your face and smashing a Halt Button when a package is lost (`throw`), what if they simply handed you a polite clipboard report? The report says: `[ X ] Failure: Package Lost`. 

### The Core Technical Concept
The `try/catch` pattern can feel aggressive and unpredictable. A modern, highly-professional alternative is the **Result Pattern**. Instead of throwing errors, functions return a Discriminated Union (from Module 04) detailing exactly what happened.

```typescript
// The Discriminated Union!
type Result<T> = 
  | { success: true; data: T }
  | { success: false; errorMessage: string };

function safeDivide(a: number, b: number): Result<number> {
  if (b === 0) {
    // We do NOT throw! We politely return a failure report.
    return { success: false, errorMessage: "Cannot divide by zero" };
  }
  return { success: true, data: a / b };
}

// The Caller's perspective:
const result = safeDivide(10, 0);

if (result.success) {
  console.log("Answer is:", result.data); // Safe to access!
} else {
  console.log("Failed politely:", result.errorMessage); // Safe to access!
}
```

### Why Production Codebases Rely on This
In massive enterprise applications, `throw` statements can cause hidden crashes because the compiler cannot force a developer to write a `try/catch` block. 
If you return a `Result<T>` union, TypeScript will literally refuse to let the developer read the `.data` until they write an `if (result.success)` statement. It forces safety at compile-time!

---

## 8. Never Swallow Errors Silently

### The Core Technical Concept
The absolute worst sin a developer can commit is writing an empty `catch` block.

```typescript
// A FIRABLE OFFENSE:
try {
  saveUserToDatabase();
} catch (error) {
  // You hid the error. If the database is broken, nobody will ever know. 
  // The user will think their data was saved, and the company will lose millions.
}
```

Even if you don't know how to fix the error, you MUST at least log it.
```typescript
// THE BARE MINIMUM:
try {
  saveUserToDatabase();
} catch (error) {
  console.error("CRITICAL: Failed to save user!", error);
}
```

---

## 9. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **The `unknown` Catch Trap:** Never write `catch (e) { console.log(e.message) }`. Since `e` is `unknown`, this will crash if someone threw a string! Always wrap it in `if (e instanceof Error)`.
2. **Abusing Try/Catch for Control Flow:** Do not use `throw` and `catch` for normal business logic (like checking if an array is empty). Throwing an exception is computationally expensive for the JavaScript engine. Only use it for truly exceptional, unexpected failures. Use normal `if` statements or the Result Pattern for expected business validations!
3. **Forgetting `finally` on Loaders:** If you turn on a UI Loading Spinner before a `try` block, and you put the "turn off spinner" code inside the `try` block, what happens if an error is thrown? Execution jumps to `catch`, the spinner code is skipped, and the user is stuck with an infinite loading wheel forever! Always turn off loading spinners inside `finally` blocks!
