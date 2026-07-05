# Question 03: Multiple Type Variables (`<T, K, V>`)

Examine why enterprise architectures require declaring multiple independent generic type parameters, and how they preserve relationships across heterogeneous data structures.

## Code Scenario

Consider a universal key-value mapping utility designed to pair arbitrary keys with arbitrary values:

```typescript
interface KeyValuePair<K, V> {
  key: K;
  value: V;
}

function createKeyValuePair<K, V>(key: K, value: V): KeyValuePair<K, V> {
  return { key: key, value: value };
}

const userScore = createKeyValuePair<string, number>("alice_score", 1500);
const statusFlag = createKeyValuePair<number, boolean>(404, false);
```

## Conceptual Questions

1. Why is it architecturally necessary to declare two distinct type parameters (`<K, V>`) for a key-value structure rather than using a single type parameter (like `KeyValuePair<T>`)? What would happen if we used only `<T>`?
2. In the `statusFlag` instantiation above, what exact types are bound to `K` and `V`? Can another developer subsequently instantiate `KeyValuePair<boolean, string[]>` without modifying the original interface blueprint? Why?
3. In your own words, explain how multiple type variables enable multi-type relationship tracking, and list the standard engineering letter conventions used for primary types, property keys, dictionary values, and array elements.

## ANSWER HERE

> **1. Why two distinct type parameters `<K, V>` are necessary:**

> **2. Type bindings for `statusFlag` and independent instantiation analysis:**

> **3. Multi-type relationship tracking and letter conventions:**
