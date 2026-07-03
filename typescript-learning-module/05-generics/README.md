# Module 05: Generics

So far, every function or interface we wrote was tied to a specific type. A function that adds numbers only works with numbers. A function that uppercases words only works with strings. Generics solve this by letting you write functions and interfaces that work with any type while still maintaining full type safety.

---

## 1. The Problem Generics Solve

Imagine you need a function that returns the first item in an array. Without generics, you might be tempted to use `any`
```typescript
function getFirst(arr: any[]): any {
  return arr[0];
}

let first = getFirst(["apple", "banana"]); // TypeScript thinks 'first' is 'any'.
first.toFixed(2); // No error from TypeScript, but this CRASHES at runtime
```

Using `any` loses all type information. TypeScript can no longer help you.

With a generic, you can write the function once and have it work with any type while preserving that type throughout
```typescript
function getFirst<T>(arr: T[]): T | undefined {
  if (arr.length === 0) return undefined;
  return arr[0];
}

let firstStr = getFirst(["apple", "banana"]); // TypeScript knows this is string | undefined.
let firstNum = getFirst([10, 20, 30]);         // TypeScript knows this is number | undefined.
```

The `<T>` is a **type variable**. It is a placeholder that TypeScript fills in with the actual type when the function is called.

---

## 2. What `<T>` Means

`T` is just a conventional name. It stands for "Type." You could name it anything, but `T` is what the industry uses by default.

When you write `function getFirst<T>`, you are saying: "This function has a type variable called `T`. TypeScript will figure out what `T` actually is when someone calls this function."

When you call `getFirst(["apple", "banana"])`, TypeScript sees that the array contains strings, so it infers `T = string`. The return type becomes `string | undefined` automatically. You rarely need to specify `T` manually.

If you want to specify it explicitly, you can
```typescript
let result = getFirst<string>(["apple", "banana"]); // Explicitly setting T = string.
```

---

## 3. Generic Functions in Practice

Here is how you would write a function that swaps two values
```typescript
function swap<A, B>(first: A, second: B): [B, A] {
  return [second, first];
}

let swapped = swap("hello", 42); // TypeScript infers A = string, B = number.
// swapped is typed as [number, string]
```

You can use multiple type variables (`A`, `B`, `C`, etc.) when a function deals with more than one independent type.

---

## 4. Tuples

Before continuing with generics, it is useful to understand **tuples**. A tuple is an array where the number of items and the type of each item at each position is fixed
```typescript
let pair: [string, number] = ["Alice", 30];
// pair[0] is always a string.
// pair[1] is always a number.
// pair[2] would be an error.
```

Tuples are useful when you want to return two related values from a function without creating a full interface
```typescript
function getNameAndAge(): [string, number] {
  return ["Alice", 30];
}

let [name, age] = getNameAndAge();
```

---

## 5. Generic Constraints (`extends`)

By default, `<T>` accepts absolutely any type. But sometimes your function needs the type to have at least certain properties. You constrain the generic using the `extends` keyword
```typescript
// Without a constraint, TypeScript does not know if T has a .length property.
// function printLength<T>(item: T): void { console.log(item.length); } // ERROR
// With a constraint, we guarantee T must have a 'length' property
function printLength<T extends { length: number }>(item: T): void {
  console.log(item.length);
}

printLength("Hello");    // Valid. Strings have .length.
printLength([1, 2, 3]);  // Valid. Arrays have .length.
// printLength(42);      // ERROR! Numbers do not have .length.
```

The constraint `<T extends { length: number }>` means "T can be any type, as long as it has a `length` property that is a number."

---

## 6. Multiple Generic Type Variables

You can define more than one type variable when different parts of a function deal with independently varying types
```typescript
type Pair<K, V> = {
  key: K;
  value: V;
};

const record1: Pair<string, number>  = { key: "score", value: 99 };
const record2: Pair<number, boolean> = { key: 1, value: true };
```

`K` and `V` are independent. The type you choose for `K` does not affect what you can choose for `V`.

---

## 7. Generic Interfaces and Default Types

Interfaces can also use generic type variables. This allows you to create reusable shapes that work with different data types
```typescript
interface ApiResponse<T> {
  success: boolean;
  data: T;
  timestamp: Date;
}

// When you use this interface, you specify what T is
type UserResponse  = ApiResponse<{ id: string; name: string }>;
type NumberResponse = ApiResponse<number>;
```

You can also set a **default type** for a generic. If the caller does not specify one, the default is used
```typescript
interface PaginatedResponse<T = string> {
  items: T[];
  currentPage: number;
  totalPages: number;
}

// Uses the default (T = string)
const strPage: PaginatedResponse = { items: ["a", "b"], currentPage: 1, totalPages: 3 };

// Overrides the default with a custom type
const userPage: PaginatedResponse<{ id: number; name: string }> = {
  items: [{ id: 1, name: "Alice" }],
  currentPage: 1,
  totalPages: 5
};
```

---

## 8. Generic Type Inference

In most cases you do not need to manually write the type argument when calling a generic function. TypeScript inspects the actual argument you pass and figures out the type variable automatically
```typescript
function identity<T>(value: T): T {
  return value;
}

// TypeScript automatically figures out T = string here
let a = identity("hello");

// TypeScript automatically figures out T = number here
let b = identity(42);

// You can still write it explicitly if you need to
let c = identity<boolean>(true);
```

This automatic inference is called **generic argument inference**. It is why most generic function calls look just like regular function calls.

---

## 9. Real-World Use Cases and Common Pitfalls

### Real-World Use Case 1: Reusable HTTP API Wrappers (`ApiResponse<T>`)
Every enterprise web application communicates with servers. Instead of writing separate interfaces for `UserResponse`, `ProductResponse`, and `OrderResponse`, engineers write a single generic `ApiResponse<T>` wrapper.

```typescript
interface ApiResponse<T> {
  success: boolean;
  errorCode?: number;
  data: T;
}

// Reusing the wrapper for any data type
type UserListResponse = ApiResponse<string[]>;
type OrderResponse = ApiResponse<{ orderId: number; total: number }>;
```

### Real-World Use Case 2: Frontend State Management Hooks (`useState<T>`)
In React or Next.js applications, state containers use generics so that when you store a list of tasks or a logged-in user profile, TypeScript knows exactly what properties exist on your state object.

### Common Pitfall to Avoid: Adding Meaningless Generics
A generic type variable `T` is only useful if it relates two or more places (like relating an input argument to a return type). If a type variable only appears once, it does nothing that `unknown` or `any` could not do. Keep your generics focused and purposeful!
