# Senior Technical Interview Review & Architecture Masterclass

This review module steps back from syntax mechanics and evaluates the entire TypeScript curriculum through the rigorous lens of a **Principal/Senior Systems & Architecture Interview**.

In junior interviews, engineers are evaluated on syntax recognition (`"What is an interface?"`). In senior engineering interviews, candidates are evaluated on **runtime implications, system boundaries, architectural resilience, and compiler theory**. Interviewers test whether you understand what TypeScript *cannot* do just as deeply as what it can do.

This document synthesizes Modules 01 through 11 into deep architectural mental models designed to ace technical system design rounds.

---

## 1. Type Erasure & The Boundary Vulnerability Principle (Modules 01, 04, 08)

The foundational concept of TypeScript compilation is **Type Erasure**. Every type annotation, interface, type alias, generic `<T>`, and type assertion (`as`) exists exclusively at compile time. When the TypeScript compiler (`tsc`) transforms your code into executable output for Node.js or browsers, **100% of the type system is stripped away**.

### The Senior Interview Scenario
> *"A developer writes an Express API endpoint that casts incoming HTTP request bodies using `const payload = req.body as CreateOrderInput;`. In code review, why must you block this pull request even if `strict: true` is enabled across the entire project?"*

### The Architectural Analysis
The `as` keyword does not perform runtime type verification or transformation; it is a **compiler silence directive**. It tells `tsc`: *"Suspend static checking on this expression; assume I have verified the memory shape."*

Because HTTP bodies arrive over a network boundary as unverified JSON strings, casting them creates a silent divergence between the compile-time contract and runtime reality. If an API client sends `{ "amount": "1000" }` (string) instead of `{ "amount": 1000 }` (number), TypeScript compiles cleanly. At runtime, when your business logic executes `payload.amount.toFixed(2)`, Node.js throws an unhandled `TypeError: payload.amount.toFixed is not a function`, crashing the server.

```typescript
// ANTI-PATTERN: Dangerous Boundary Casting
async function createOrderHandler(req: Request, res: Response): Promise<void> {
  const payload = req.body as { orderId: string; amount: number };
  // If req.body is missing 'amount', this throws a fatal TypeError at runtime
  const tax = payload.amount * 0.08;
}

// PRODUCTION PATTERN: Explicit Runtime Boundary Validation
function isCreateOrderInput(raw: unknown): raw is { orderId: string; amount: number } {
  return (
    typeof raw === "object" &&
    raw !== null &&
    "orderId" in raw &&
    typeof (raw as Record<string, unknown>).orderId === "string" &&
    "amount" in raw &&
    typeof (raw as Record<string, unknown>).amount === "number"
  );
}

async function secureOrderHandler(req: Request, res: Response): Promise<void> {
  if (!isCreateOrderInput(req.body)) {
    res.status(400).json({ error: "Invalid payload schema." });
    return;
  }
  // Inside this block, TypeScript automatically narrows req.body to verified types
  const tax = req.body.amount * 0.08;
}
```

**Architectural Rule:** Never use `as` assertions on external boundaries (API endpoints, database query returns, file reads, localStorage, or third-party webhooks). Boundary layers must use type guards (`typeof`, `in`), custom predicates (`is`), or runtime parsing libraries like Zod.

---

## 2. Structural vs. Nominal Typing & Branded Types (Module 02)

TypeScript operates on **Structural Typing** (also called Duck Typing), whereas enterprise backend languages like Java, C#, and Rust enforce **Nominal Typing**.

### The Senior Interview Scenario
> *"Explain why structural typing allows passing an instance of `class Dog` into a function expecting `class Cat`. Then, explain how enterprise banking systems use Branded Types to enforce nominal isolation on primitive strings."*

### The Architectural Analysis
Under nominal typing, two types are compatible only if their declarations explicitly declare an inheritance or interface relationship (`class Dog implements Cat`). Under structural typing, TypeScript compares **shape only**. If `Cat` requires `{ name: string; meow(): void }` and `Dog` contains those exact property names and function signatures, TypeScript considers them completely identical.

While structural typing makes UI component composition and mocking effortless, it introduces dangerous vulnerabilities in high-security domain logic
```typescript
// Structural Vulnerability in Financial Code
type AccountId = string;
type TransactionId = string;

function executeTransfer(fromAccount: AccountId, transactionRef: TransactionId): void {
  // Business logic...
}

const accId: AccountId = "ACC-99182";
const txId: TransactionId = "TX-00412";

// COMPILES CLEANLY despite catastrophic domain mix-up
executeTransfer(txId, accId);
```

To eliminate structural aliasing bugs, senior architectures implement **Branded Types** (Phantom Types). By intersecting a primitive string with an object containing a unique string tag or `unique symbol`, TypeScript treats identical primitives as completely distinct types
```typescript
export type Brand<K, T> = K & { readonly __brand: T };

export type AccountId = Brand<string, "AccountId">;
export type TransactionId = Brand<string, "TransactionId">;

export function createAccountId(id: string): AccountId {
  if (!id.startsWith("ACC-")) throw new Error("Invalid account ID format.");
  return id as AccountId;
}

export function createTransactionId(id: string): TransactionId {
  if (!id.startsWith("TX-")) throw new Error("Invalid transaction ID format.");
  return id as TransactionId;
}

// Now, swapping arguments triggers an immediate compile-time failure
const safeAcc = createAccountId("ACC-99182");
const safeTx = createTransactionId("TX-00412");

// executeTransfer(safeTx, safeAcc);
// Argument of type 'Brand<string, "TransactionId">' is not assignable to parameter of type 'Brand<string, "AccountId">'.
```

---

## 3. Discriminated Unions & Exhaustiveness Guarding (Module 04)

In complex domain modeling, seniors evaluate whether code permits **impossible states**.

### The Senior Interview Scenario
> *"Why is declaring boolean flags like `isLoading: boolean; isError: boolean; data?: User;` considered an architectural anti-pattern? How does a Discriminated Union combined with the `never` bottom type guarantee long-term workflow stability?"*

### The Architectural Analysis
An interface with 3 boolean flags allows $2^3 = 8$ possible combinations, yet only 3 states are logically valid in reality (`Loading`, `Success`, `Failure`). The remaining 5 combinations (`isLoading: true, isError: true, data: [...]`) represent corrupted state space that causes UI flickering and null-pointer exceptions.

By refactoring into a **Discriminated Union**, every state explicitly defines its allowed data payload, completely locking out invalid combinations. When combined with an exhaustiveness check using the `never` type, the compiler becomes an automated regression guard
```typescript
type PaymentState =
  | { status: "idle" }
  | { status: "processing"; gatewayId: string }
  | { status: "completed"; transactionRef: string; chargedAmount: number }
  | { status: "failed"; errorCode: number; reason: string };

function renderPaymentStatus(state: PaymentState): string {
  switch (state.status) {
    case "idle"
      return "Enter card details to proceed.";
    case "processing"
      return `Connecting to gateway ${state.gatewayId}...`;
    case "completed"
      return `Success! Ref: ${state.transactionRef} ($${state.chargedAmount})`;
    case "failed"
      return `Error [Code ${state.errorCode}]: ${state.reason}`;
    default
      // If a teammate adds { status: "refunded" } to PaymentState 1 year later
      // and forgets to update this function, TypeScript immediately halts compilation
      // Type '({ status: "refunded" })' is not assignable to type 'never'.
      const _exhaustiveGuard: never = state;
      return _exhaustiveGuard;
  }
}
```

---

## 4. Advanced Generics & Inference Mechanics (Modules 05, 06)

Generics separate novice code (which relies on concrete duplication or `any`) from production-grade libraries.

### The Senior Interview Scenario
> *"Why does `function getProperty<T, K extends keyof T>(obj: T, key: K): T[K]` provide perfect type safety compared to taking `(obj: Record<string, any>, key: string)`?"*

### The Architectural Analysis
Using `Record<string, any>` erases the relationship between the specific object property and its return value. A caller extracting `.age` from a user object receives `any`, allowing illegal operations like `.toLowerCase()` on a numeric age.

By linking `K extends keyof T`, TypeScript enforces two compile-time guarantees
1. `key` must exactly match an existing property name on object `T`. Typos are rejected immediately.
2. The return type indexed access `T[K]` preserves exact property typing. If `obj.age` is a `number`, the return signature resolves strictly to `number`.

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { username: "alex_dev", age: 31, isVerified: true };

const name = getProperty(user, "username"); // Inferred strictly as string
const age = getProperty(user, "age");       // Inferred strictly as number

// COMPILE ERROR: Argument of type '"password"' is not assignable to parameter of type '"username" | "age" | "isVerified"'.
// const pass = getProperty(user, "password");
```

---

## 5. Clean Layer Decomposition & The 300-Line Rule (Module 09)

System architecture rounds focus on codebase longevity and scalability.

### The Senior Interview Scenario
> *"You are tasked with reviewing an Express backend where single files routinely exceed 700 lines, mixing HTTP header extraction, SQL query strings, validation logic, and third-party email notifications. How do you refactor this using Separation of Concerns?"*

### The Architectural Analysis
Monolithic logic files violate the Single Responsibility Principle (SRP), making automated unit testing impossible because testing business math requires mocking HTTP sockets and SQL connections.

Production architectures enforce strict dependency layers pointing inward
```
[ Transport Layer (HTTP / CLI) ]
             │
             ▼
[ Service Layer (Pure Business Logic) ]
             │
             ▼
[ Repository Layer (Data Access / I/O) ]
```

1. **Repository Layer (`repositories/userRepo.ts`)**: Executes raw SQL queries or ORM calls. It returns pure domain entities. It has zero knowledge of HTTP request objects or business validation rules.
2. **Service Layer (`services/userService.ts`)**: Contains 100% of domain rules (tax math, account verification). It accepts domain entities, calls repositories, and returns domain results. It can be unit-tested in complete isolation with fast in-memory mock repositories.
3. **Transport Layer (`controllers/userController.ts`)**: Thin orchestration. Extracts HTTP headers, invokes the service layer, and translates return values into HTTP status codes (`200 OK`, `400 Bad Request`).

**The 300-Line Rule:** If any single logic file exceeds 300 lines, it is almost certainly violating SRP by handling multiple responsibilities. Split proactively into domain-specific modules.

---

## 6. Concurrency & Event Loop Mechanics (Module 10)

Senior backend engineers must understand Node.js event loop scheduling to prevent performance bottlenecks.

### The Senior Interview Scenario
> *"Analyze the performance impact of `for (const id of userIds) { await fetchUser(id); }` versus `await Promise.all(userIds.map(id => fetchUser(id)))`. When is `Promise.allSettled` mandatory?"*

### The Architectural Analysis
- **Sequential Blocking (`for...of` with `await`)**: Halts execution flow at each iteration. If `fetchUser` takes 200ms over network latency and the array contains 20 items, the loop blocks execution for $20 \times 200\text{ms} = 4,000\text{ms}$ (4 seconds).
- **Parallel Concurrency (`Promise.all`)**: Dispatches all 20 network requests simultaneously across Node.js I/O threads. Total execution time equals the slowest single request (~200ms) - a 20x throughput improvement. However, if request #19 fails with a 500 Server Error, `Promise.all` immediately rejects, discarding the 19 successful responses.
- **Resilient Batching (`Promise.allSettled`)**: Dispatches all 20 requests concurrently and guarantees that all promises settle regardless of individual rejections. It returns an array of typed settlement objects (`{ status: "fulfilled", value } | { status: "rejected", reason }`). This is mandatory in data ingestion pipelines or UI dashboards where partial success is acceptable.

---

## 7. The Result Pattern vs. Exceptions (Module 11)

Throwing exceptions across complex system boundaries is widely considered an anti-pattern in mission-critical TypeScript.

### The Senior Interview Scenario
> *"Why do modern TypeScript engines model errors as return values (`Result<T, E>`) instead of relying on `throw new Error()`?"*

### The Architectural Analysis
Standard exceptions (`try/catch`) suffer from two severe compiler flaws
1. **Signature Invisibility**: Looking at `function chargeCard(amount: number): Promise<Receipt>`, the caller has zero indication that the function might throw `CardDeclinedError` or `GatewayTimeoutError`.
2. **Untyped Catch Blocks**: Inside a `catch (err: unknown)` block, TypeScript cannot infer what error type occurred, forcing repetitive runtime `instanceof` checks.

By modeling errors as explicit domain values using the **Result Pattern**, failure possibilities become documented, type-checked contracts embedded directly in the return type
```typescript
export type Result<T, E = string> =
  | { success: true; data: T }
  | { success: false; error: E; code?: string };

export async function processTransaction(amount: number): Promise<Result<string, "INSUFFICIENT_FUNDS" | "GATEWAY_DOWN">> {
  if (amount > 5000) {
    return { success: false, error: "Balance limit exceeded.", code: "INSUFFICIENT_FUNDS" };
  }
  return { success: true, data: "TXN_88192" };
}

// Callers are forced by the compiler to check .success before reading .data
async function handleCheckout() {
  const res = await processTransaction(6000);
  if (!res.success) {
    // TypeScript knows res.error exists and res.code is strictly typed
    console.error(`Checkout failed [${res.code}]: ${res.error}`);
    return;
  }
  console.log(`Receipt: ${res.data}`);
}
```

---

## 8. Top Senior Technical Interview Questions & Model Answers

### Q1: What is the exact difference between `any` and `unknown`?
**Model Answer:** Both accept any value at assignment. `any` disables static type checking entirely, allowing arbitrary property accesses and method calls that can crash at runtime. `unknown` is the type-safe counterpart; the compiler blocks all property accesses, invocations, and assignments until the value is explicitly narrowed via type guards (`typeof`, `instanceof`) or validation functions.

### Q2: What are index signatures and when do they cause runtime risks?
**Model Answer:** Index signatures (`[key: string]: number`) allow objects to hold arbitrary dynamic keys. The runtime risk is that TypeScript assumes any requested key returns a valid `number`, even if the key does not exist (`obj["missing"] === undefined`). To make index signatures safe under `strictNullChecks`, always include `undefined` in the value union: `[key: string]: number | undefined`.

### Q3: Explain how `readonly` differs on interfaces versus `as const` assertions.
**Model Answer:** Applying `readonly` to an interface property prevents reassigning that specific property reference (`user.name = "Bob"` fails). However, if the property is a nested array or object, its internal contents remain mutable (`user.tags.push("new")` succeeds). Applying `as const` to an object literal recursively locks every nested property, array, and literal value into a deeply immutable, read-only structure.

### Q4: Why can callers never invoke a function's implementation signature when overload signatures exist?
**Model Answer:** When TypeScript processes overloaded functions, the implementation signature acts strictly as the internal bridge uniting all external overload definitions. To ensure callers only provide validated parameter combinations, the compiler restricts external invocations exclusively to the published overload signatures.

### Q5: What is the difference between `Promise.all` and sequential `await` in loops?
**Model Answer:** Sequential `await` inside a `for...of` loop executes async operations serially, causing latency accumulation ($N \times \text{delay}$). `Promise.all` dispatches all promises concurrently, reducing total duration to the latency of the single slowest operation.
