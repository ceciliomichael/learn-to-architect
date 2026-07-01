# Option 10: In-Memory Key-Value Database with TTL & ACID Transactions (Mini-Redis)

**Difficulty:** Advanced
**Primary Concepts:** Generics, deep serialization/cloning, async timers, ACID transaction isolation, rollback logic

---

## Why This Matters

Databases like Redis and SQLite handle millions of operations per second while guaranteeing that transactions either fully succeed or completely roll back on error. Building an in-memory database engine forces you to handle memory leaks (cleaning up expired TTL timers), object mutations (preventing callers from mutating stored references), and transaction snapshot isolation.

---

## Domain & Core Requirements

Build a `MemoryDB` class supporting generic stored values:

```typescript
set<T>(key: string, value: T, ttlMs?: number): void
// Stores a deep-cloned copy of value. If ttlMs is provided, automatically deletes the key after duration.

get<T>(key: string): T | undefined
// Returns deep-cloned copy of value so callers cannot mutate internal storage.
// Returns undefined if key does not exist or has expired.

delete(key: string): boolean

exists(key: string): boolean

clear(): void
// Removes all keys and clears all active TTL timers to prevent memory leaks.
```

---

## Transaction Engine (ACID Simulation)

Implement multi-step atomic transactions:

```typescript
async transaction<T>(callback: (tx: TransactionScope) => Promise<T>): Promise<Result<T>>
```

Inside `callback`:
1. `tx` exposes `.get()`, `.set()`, and `.delete()`.
2. All modifications made inside `tx` are buffered in an isolated snapshot.
3. If `callback` finishes successfully, the buffered mutations are **committed** to the main DB atomically.
4. If `callback` throws any error or rejects, all buffered mutations are **discarded (rolled back)** immediately, leaving the main DB untouched.

---

## What Your Final index.ts Should Demonstrate

1. Store user profiles and account balances.
2. Demonstrate TTL expiration by storing a session key with `ttlMs: 200`, waiting 300ms using `setTimeout`/Promise, and verifying `get()` returns `undefined`.
3. Execute a successful bank transfer transaction between User A and User B.
4. Execute a failing bank transfer transaction (where User A has insufficient balance halfway through)  -  verify that User A's deducted balance rolls back completely!
