# Module 04: Exercise Solutions and Architectural Master Guide

Welcome to the comprehensive master solution guide for **Module 04: Advanced Types and Narrowing**. This document provides production-grade reference implementations, deep conceptual analysis, and architectural comparisons for all three lab challenges.

---

## 1. Challenge 01 Solution: Narrowing Multiple Types

This challenge demonstrates how to use TypeScript's Control Flow Analysis (CFA) with primitive `typeof` type guards to narrow a multi-type union safely.

```typescript
/**
 * Evaluates an input primitive value and returns a descriptive string formatting.
 * Demonstrates sequential type pruning using typeof guards.
 */
function describeInput(value: string | number | boolean): string {
  // Gate 1: Check for primitive string
  if (typeof value === "string") {
    // CFA narrows 'value' to 'string'. Safe to access '.length'.
    return `Text with ${value.length} characters: ${value}`;
  } 
  // Gate 2: Check for primitive number
  else if (typeof value === "number") {
    // CFA narrows 'value' to 'number'. Safe to call '.toFixed(2)'.
    return value.toFixed(2);
  } 
  // Gate 3: Residual deduction
  else {
    // CFA knows only 'boolean' remains in the union.
    return value === true ? "Enabled" : "Disabled";
  }
}

// Verification Logs
console.log(describeInput("TypeScript Lab")); // "Text with 14 characters: TypeScript Lab"
console.log(describeInput(100.456));          // "100.46"
console.log(describeInput(true));             // "Enabled"
```

### Architectural Key Takeaway
When working with primitive unions (`string | number | boolean`), **always use `typeof` checks inside standard `if / else if / else` control flow structures**. TypeScript's compiler automatically tracks branch execution paths and narrows variable types without requiring manual type assertions or casting.

---

## 2. Challenge 02 Solution: Discriminated Union State Machine

This challenge demonstrates modeling asynchronous workflows using Tagged Unions and enforcing compile-time exhaustiveness checking with the `never` bottom type.

```typescript
/**
 * Mutually exclusive lifecycle states for a file processing operation.
 * Every constituent shares the string literal discriminator tag: 'status'.
 */
type FileOperationResult =
  | { status: "idle" }
  | { status: "processing"; filename: string; progress: number }
  | { status: "complete";   filename: string; sizeBytes: number };

/**
 * Formats status reports using a discriminated union switch statement.
 * Includes an automated compile-time safety trap for unhandled states.
 */
function reportStatus(state: FileOperationResult): string {
  switch (state.status) {
    case "idle":
      return "No operation running.";

    case "processing":
      // Narrows to processing state; safe to access filename and progress.
      return `Processing ${state.filename}: ${state.progress}% done.`;

    case "complete":
      // Narrows to complete state; safe to access filename and sizeBytes.
      return `${state.filename} completed. Size: ${state.sizeBytes} bytes.`;

    default:
      // Compile-Time Circuit Breaker:
      // If all union members are handled above, 'state' is narrowed to 'never'.
      // If an unhandled state reaches this point, the compiler throws a build error!
      const exhaustiveCheck: never = state;
      return exhaustiveCheck;
  }
}

// Verification Logs
console.log(reportStatus({ status: "idle" }));
console.log(reportStatus({ status: "processing", filename: "archive.zip", progress: 85 }));
console.log(reportStatus({ status: "complete",   filename: "archive.zip", sizeBytes: 52428800 }));
```

### Architectural Key Takeaway
Never model complex application state using optional properties (`{ isLoading?: boolean; data?: string[] }`). **Always use Discriminated Unions with literal discriminator tags**. This makes illegal state combinations mathematically impossible and enables automated exhaustiveness checking via `never`.

---

## 3. Challenge 03 Solution: Custom Type Guard

This challenge demonstrates extracting complex narrowing logic into reusable utility functions using type predicate return signatures (`parameterName is TypeName`).

```typescript
interface PremiumUser {
  plan: "premium";
  monthlyFee: number;
  maxDownloads: number;
}

interface FreeUser {
  plan: "free";
  dailyLimit: number;
}

/**
 * Custom Type Guard: Verifies whether a user account belongs to the premium tier.
 * The signature 'user is PremiumUser' instructs the compiler to narrow across scopes.
 */
function isPremiumUser(user: PremiumUser | FreeUser): user is PremiumUser {
  return user.plan === "premium";
}

/**
 * Logs tier-specific account details by leveraging our custom type guard.
 */
function printUserInfo(user: PremiumUser | FreeUser): void {
  if (isPremiumUser(user)) {
    // Narrows strictly to PremiumUser
    console.log(`Premium user. Fee: $${user.monthlyFee.toFixed(2)}/mo. Max downloads: ${user.maxDownloads}`);
  } else {
    // Narrows strictly to FreeUser
    console.log(`Free user. Daily limit: ${user.dailyLimit} requests`);
  }
}

// Verification Logs
printUserInfo({ plan: "premium", monthlyFee: 29.99, maxDownloads: 1000 });
printUserInfo({ plan: "free",    dailyLimit: 50 });
```

### Architectural Key Takeaway
When checking interface types across multiple components or filtering arrays, **never return a plain `boolean` from validation helpers**. Always use type predicate signatures (`arg is Type`) so TypeScript's compiler can propagate type narrowing decisions cleanly into the calling scope.

---

## 4. Comprehensive Synthesis: The Three Narrowing Pillars

To architect production-grade TypeScript applications, senior engineers choose the right narrowing mechanism based on the data boundaries and runtime types involved:

| Narrowing Technique | Primary Target | Syntax Mechanics | Runtime Performance | Enterprise Best Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **Primitive Guard (`typeof`)** | Primitive values (`string`, `number`, `boolean`, `symbol`, `bigint`, `undefined`). | `if (typeof x === "string")` | **Ultra High:** Evaluates internal V8 memory type tags via high-speed bitwise operations. | Form validation, primitive argument parsing, and basic utility functions. |
| **Discriminated Union (`switch`)** | Complex object hierarchies and state machines. | `switch (obj.status)` on a shared literal property tag. | **Ultra High:** Direct property lookup optimized by V8 Hidden Class inline caches. | Asynchronous network request states, UI component lifecycle models, and Redux/Zustand action reducers. |
| **Custom Type Guard (`is`)** | Interfaces, type aliases, and external API payloads. | `function isX(val): val is X` | **High:** Executes custom developer check logic at runtime; type predicate erases completely. | Encapsulating multi-file type validation, array filtering (`arr.filter(isX)`), and API boundary validation. |

---

## 5. Debugging Guide: Resolving Common Narrowing Errors

### Error 1: `Property 'X' does not exist on type 'A | B'`
- **Root Cause:** You attempted to access a property belonging to only one member of a union before proving to the compiler which member is currently stored in the variable.
- **Production Fix:** Wrap the property access inside a narrowing gate: `if ("X" in variable)` or check a discriminator tag: `if (variable.kind === "A")`.

### Error 2: `Type 'X' is not assignable to type 'never'`
- **Root Cause:** You added a new member to a Discriminated Union type, but you forgot to add a handling `case` branch in your switch statement before reaching the `default:` exhaustiveness check.
- **Production Fix:** Add the missing `case` block to handle the new state explicitly. This error is a feature, not a bug: it protects your application from unhandled runtime states!

### Error 3: `'X' only refers to a type, but is being used as a value here`
- **Root Cause:** You wrote an `instanceof` check against a TypeScript interface: `if (data instanceof UserInterface)`.
- **Production Fix:** Remember that interfaces are completely erased during JavaScript compilation. You can only use `instanceof` with physical runtime classes (like `Date` or `Error`). For interfaces, use custom type guards or the `in` operator!
