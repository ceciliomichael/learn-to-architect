# Option 03: Type-Safe Pub/Sub Event System

**Difficulty:** Advanced
**Primary Concepts:** Advanced generics, mapped types, indexed access types, function signatures, classes

---

## Project Brief

Every major UI framework and backend architecture relies on event systems  -  emitters, listeners, channels, and hooks. The problem in standard JavaScript is that event systems are completely untyped: you emit a `"user:login"` string and pass whatever random payload object you feel like, and the listener hopes it receives the right fields.

You will build a **strictly typed event bus**. When a developer subscribes to an event name, TypeScript must automatically infer the exact payload parameter type in the callback function. If someone tries to emit an event with the wrong payload shape, the compiler must reject it immediately.

---

## The Type Safety Requirement

Given an event map like this:

```typescript
interface AppEvents {
  "user:created": { id: string; username: string; email: string };
  "user:logout":  { id: string; reason?: string };
  "order:placed": { orderId: string; total: number; itemsCount: number };
  "system:ping":  void; // No payload
}
```

Your `EventBus` must enforce these checks at **compile time**:

```typescript
const bus = new EventBus<AppEvents>();

// 1. Valid subscription  -  TypeScript infers 'payload' has orderId, total, itemsCount:
bus.on("order:placed", (payload) => {
  console.log(payload.total.toFixed(2));
});

// 2. Invalid event name  -  COMPILE ERROR:
// bus.on("user:deleted", () => {});

// 3. Invalid payload emitted  -  COMPILE ERROR (missing 'total'):
// bus.emit("order:placed", { orderId: "123", itemsCount: 5 });

// 4. Valid void event:
bus.emit("system:ping");
```

---

## Core Requirements

Build an `EventBus<TEventMap extends Record<string, any>>` class supporting:

```typescript
on<K extends keyof TEventMap>(
  event: K,
  handler: (payload: TEventMap[K]) => void | Promise<void>
): Subscription
// Subscribes a handler. Returns a Subscription object with an unsubscribe() method.

once<K extends keyof TEventMap>(
  event: K,
  handler: (payload: TEventMap[K]) => void | Promise<void>
): Subscription
// Subscribes a handler that automatically unsubscribes itself after running once.

emit<K extends keyof TEventMap>(
  ...args: TEventMap[K] extends void ? [event: K] : [event: K, payload: TEventMap[K]]
): void
// Emits synchronously. Notice the conditional rest parameter: if payload is void,
// the second argument must be omitted entirely!

async emitAsync<K extends keyof TEventMap>(
  ...args: TEventMap[K] extends void ? [event: K] : [event: K, payload: TEventMap[K]]
): Promise<EventResult[]>
// Runs all async/sync handlers and returns their settlement status using Promise.allSettled.

clear(event?: keyof TEventMap): void
// Removes all listeners for a specific event, or all listeners across all events if omitted.

listenerCount(event: keyof TEventMap): number
```

---

## Advanced Feature: Wildcard & Middleware Support

Add an `intercept` method that registers middleware running before any event is dispatched:

```typescript
type Middleware<TEventMap> = (
  event: keyof TEventMap,
  payload: unknown,
  next: () => void | Promise<void>
) => void | Promise<void>;

bus.intercept(async (event, payload, next) => {
  console.log(`[Log] Dispatching ${String(event)}`);
  const start = Date.now();
  await next();
  console.log(`[Log] Finished ${String(event)} in ${Date.now() - start}ms`);
});
```

---

## File Structure You Must Use

```
src/
├── types/
│   └── events.ts           -  Generic type definitions for listeners, event maps, subscriptions
├── bus/
│   ├── subscription.ts     -  Subscription handle class
│   └── eventBus.ts         -  Core EventBus implementation
└── index.ts                -  Demonstration with realistic app events
```

---

## What Your Final index.ts Should Demonstrate

1. Define an `ECommerceEvents` interface with at least 5 distinct event types.
2. Instantiate the bus and register a logging middleware.
3. Subscribe multiple handlers to `"order:placed"`.
4. Use `.once()` for a welcome email handler on `"user:created"`.
5. Emit events both synchronously and asynchronously (`emitAsync`).
6. Unsubscribe a handler using the returned subscription object and verify `.listenerCount()`.
