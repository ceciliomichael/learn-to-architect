# Question 02 Answer: Array Protection & `const`

## Verified Correct Answer
**No, TypeScript does NOT throw an error on the `.push()` line.**

---

## Exhaustive Architectural Explanation

### Stack Bindings vs. Heap Memory Allocation
To understand why `.push()` is permitted on a `const` array, we must examine how variables and data structures are allocated in computer memory:

1. **The Variable Binding (The Stack):** When you declare `const scores: number[] = [90, 85]`, the variable label `scores` is stored in the memory stack. This stack slot holds a **pointer reference** (an address in memory) directing the engine where to find the actual array data.
2. **The Data Structure (The Heap):** The actual array contents (`[90, 85]`) are allocated in heap memory as a dynamic collection of compartments.

### What `const` Actually Protects
The keyword `const` enforces immutability strictly on the **variable binding pointer in the stack**. It guarantees that once the variable label `scores` is attached to a specific memory address, you can never redirect that label to point to a brand new memory address.

```typescript
const scores: number[] = [90, 85];

// THIS IS BLOCKED BY THE COMPILER:
// We are attempting to redirect the variable pointer to a brand new array object in heap memory!
// scores = [100, 200]; // COMPILER ERROR: Cannot assign to 'scores' because it is a constant.
```

### What `const` Does NOT Protect
The `const` keyword does **not** freeze or lock the internal contents of the heap memory object itself! When you invoke `scores.push(100)`, you are not changing the memory address stored in `scores`. You are simply reaching along the existing pointer into heap memory and appending a new item into an open compartment slot within the existing array tray.

Because the variable pointer itself remains completely unchanged, the TypeScript compiler and JavaScript engine permit the mutation without error:

```typescript
const scores: number[] = [90, 85];

// THIS IS 100% VALID:
// We are mutating the internal contents of the existing heap object; the binding pointer is untouched.
scores.push(100); 
console.log(scores); // Outputs: [90, 85, 100]
```

---

## How to Achieve True Deep Immutability (`as const`)

In advanced enterprise architectures (such as Redux state management or functional programming pipelines), mutating array contents can cause subtle side effects and rendering bugs. If you want to lock both the variable binding **and** the internal contents of the array, you must use TypeScript's **Readonly Assertion (`as const`)**:

```typescript
// Using 'as const' converts the array into a deeply immutable, readonly tuple
const frozenScores = [90, 85] as const;

// Now, BOTH reassignment AND internal mutation are blocked by the compiler:
// frozenScores = [100];       // COMPILER ERROR: Cannot assign to 'frozenScores' because it is a constant.
// frozenScores.push(100);     // COMPILER ERROR: Property 'push' does not exist on type 'readonly [90, 85]'.
// frozenScores[0] = 99;       // COMPILER ERROR: Cannot assign to '0' because it is a read-only property.
```

---

## Symbol-by-Symbol Syntax Translation of Readonly Assertion

Let us deconstruct the deep freeze declaration symbol-by-symbol:

```typescript
const frozenScores = [90, 85] as const;
```

| Symbol / Word | Classification | Plain English Translation |
| :--- | :--- | :--- |
| `const` | Language Command | Allocate a permanent, un-reassignable pointer binding in stack memory. |
| `frozenScores` | Custom Identifier | Attach the developer-chosen name `frozenScores` to this pointer binding. |
| `=` | Assignment Operator | Point this binding to the memory structure evaluated on the right. |
| `[` | Array Literal Start | Open an array sequence in heap memory. |
| `90, 85` | Integer Literals | The initial numeric values occupying index slots `0` and `1`. |
| `]` | Array Literal End | Close the array sequence. |
| `as` | Type Assertion Keyword | Instruct the compiler to apply a specific structural interpretation to the preceding value. |
| `const` | Literal Type Modifier | Lock the array structure as a readonly tuple where no properties or elements can ever be mutated. |
| `;` | Terminator | End of statement. |

---

## Summary of Architectural Best Practices
* Use standard `const` for everyday arrays where the container reference must remain stable but items are dynamically added or removed during execution.
* Use `as const` (or explicit `readonly number[]` annotations) for fixed configuration lists, action types, or state trees where mutation would violate domain integrity.
