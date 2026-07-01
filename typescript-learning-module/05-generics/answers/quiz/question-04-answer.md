# Question 04  -  Answer: Tuple Types vs. Union Arrays

## Answer

### What is a tuple type?

A **tuple** is an array type where:
- The **number of elements is fixed**
- The **type of each element at each position is known**

```typescript
let pair: [string, number] = ["Alice", 30];
// pair[0] → string (always)
// pair[1] → number (always)
// pair[2] → TypeError: Tuple type '[string, number]' of length '2' has no element at index '2'.
```

### How `[string, number]` differs from `(string | number)[]`

| | `[string, number]` | `(string | number)[]` |
|--|--|--|
| Length | Fixed at exactly 2 | Any length (0, 1, 100…) |
| `[0]` type | `string` | `string \| number` |
| `[1]` type | `number` | `string \| number` |
| Extra elements | Compile error | Allowed |
| Positional safety | Full  -  TypeScript knows each slot | None  -  every slot is the union |

```typescript
let a: [string, number] = ["Alice", 30];
let b: (string | number)[] = ["Alice", 30];

// What TypeScript knows about index 0:
const nameA = a[0]; // type: string ✓
const nameB = b[0]; // type: string | number  -  you must narrow before using as string

nameA.toUpperCase();          // OK  -  TypeScript knows it's a string
nameB.toUpperCase();          // Error  -  could be number at runtime
(nameB as string).toUpperCase(); // Forced cast required, losing safety
```

### A concrete scenario where tuples are the right choice

**Returning two related values from a function without a full interface:**

```typescript
function parseCoordinate(input: string): [number, number] {
  const [lat, lng] = input.split(",").map(Number);
  return [lat, lng];
}

const [latitude, longitude] = parseCoordinate("51.5074,-0.1278");
// latitude → number
// longitude → number
// No cast needed, no wrapper object needed.
```

Using `(number | number)[]` (i.e., `number[]`) here would work at runtime, but TypeScript loses the guaranteed two-element structure. Using a tuple makes the contract explicit: callers and readers know the function always returns exactly `[latitude, longitude]`.

### Other common real-world uses

- React's `useState` returns `[state, setter]`  -  a tuple of two independently typed values
- CSV row parsing: `[string, string, number]` for `[firstName, lastName, age]`
- Key-value pairs: `[string, unknown]` in `Object.entries()`
