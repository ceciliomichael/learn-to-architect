# Option 08: Type-Safe Finite State Machine Engine (Mini-XState)

**Difficulty:** Advanced
**Primary Concepts:** Mapped types, conditional types, literal strings, generics, transition guards

---

## Why This Matters

User interfaces, checkout flows, multi-step wizards, and backend job processors are infamous for "impossible states" (e.g., showing a loading spinner while submitting an already cancelled order). **Finite State Machines (FSMs)** guarantee mathematically that your program can only be in one valid state at a time.

Building a type-safe FSM engine (inspired by XState) tests your ability to make TypeScript enforce valid transitions at compile time.

---

## The Type Safety Requirement

You must build a `StateMachine` engine where
1. You can only send events that are valid for the machine.
2. The state machine tracks context (data payload that evolves over time).

```typescript
interface MachineConfig<TContext, TState extends string, TEvent extends { type: string }> {
  id: string;
  initial: TState;
  context: TContext;
  states: Record<TState, {
    on?: {
      [E in TEvent["type"]]?: {
        target: TState;
        guard?: (ctx: TContext, event: Extract<TEvent, { type: E }>) => boolean;
        action?: (ctx: TContext, event: Extract<TEvent, { type: E }>) => TContext;
      };
    };
  }>;
}
```

---

## Core Requirements

Build the `StateMachineInstance<TContext, TState, TEvent>` class
```typescript
send(event: TEvent): Result<{ state: TState; context: TContext }>
// Attempts to transition state
// 1. Checks if current state has a transition for event.type.
// 2. If transition has a guard function, executes guard. If false, returns error: "GUARD_REJECTED".
// 3. If transition has an action, executes action to update immutable context.
// 4. Updates current state to target.

subscribe(listener: (state: TState, context: TContext) => void): () => void
// Pub/Sub listener notified whenever state or context changes.

getState(): TState
getContext(): TContext
```

---

## What Your Final index.ts Should Demonstrate

Build a **Payment Processing Workflow Machine**
- States: `"idle" | "validating" | "charging" | "success" | "failed"`
- Events
  - `{ type: "SUBMIT"; amount: number; cardNumber: string }`
  - `{ type: "VALIDATION_SUCCESS" }`
  - `{ type: "CHARGE_SUCCESS"; transactionId: string }`
  - `{ type: "FAIL"; reason: string }`
  - `{ type: "RETRY" }`

Demonstrate
1. Attempting to transition from `"idle"` to `"success"` directly  -  verify your machine rejects it.
2. Passing through `"idle"` -> `"validating"` -> `"charging"` -> `"success"` cleanly.
3. Using a guard on `"SUBMIT"` that rejects amounts <= 0.
