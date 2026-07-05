# Module 05: Generics

In previous modules, every function and interface we built was permanently locked to a specific data type. A function that capitalizes text only works with `string`. A function that calculates tax only works with `number`. 

But what if you need to build a function that can process *any* type of data, while still guaranteeing 100% type safety? This module introduces **Generics**—the mechanism that allows you to write flexible, reusable blueprints without sacrificing strict type rules.

---

## 1. The Problem Generics Solve

### The Real-World Analogy: The Blank Shipping Box
Imagine you own a shipping company. You have thousands of customers shipping different items: books, laptops, and shoes.
If you didn't have generics, you would have to manufacture a special "Book Box", a special "Laptop Box", and a special "Shoe Box". Building a custom box for every possible item in the universe is exhausting and repetitive.

Instead, you manufacture a single **Generic Blank Box** with a clear plastic label pouch on the outside. When a customer ships an item, they slide a paper label into the pouch saying "Contains: Laptops". Now, everyone in the shipping pipeline knows exactly what is inside the box, even though the physical cardboard box is identical for everyone.

### The Core Technical Concept
Imagine we want to write a simple function that returns the very first item in an array.

If we don't use Generics, we might be tempted to use the dangerous `any` wildcard type to make the function accept any array:

```typescript
// BAD: Using 'any' destroys all type safety!
function getFirst(arr: any[]): any {
  return arr[0];
}

// TypeScript is blind here. It thinks 'firstItem' is 'any'.
let firstItem = getFirst(["apple", "banana"]); 

// TypeScript will NOT warn you about this, and it will CRASH at runtime!
firstItem.toFixed(2); 
```

**Generics** solve this. A Generic is a variable for a *type*, rather than a variable for *data*. 

```typescript
// GOOD: Using a Generic <T> to preserve exact type safety
function getFirst<T>(arr: T[]): T | undefined {
  if (arr.length === 0) return undefined;
  return arr[0];
}

// TypeScript looks at the input array of strings.
// It automatically swaps out <T> for <string>.
// It knows for absolute certain that 'firstStr' is a string!
let firstStr = getFirst(["apple", "banana"]); 

// firstStr.toFixed(2); // COMPILER ERROR: Property 'toFixed' does not exist on type 'string'.
```

---

## 2. What `<T>` Means

### The Core Technical Concept
The `<T>` syntax is a **Type Variable**. 
Just like `let x = 5` creates a variable `x` that holds data, `<T>` creates a variable `T` that holds a type (like `string` or `number`).

* `T` is just a custom label! It stands for "Type". You could literally name it `<MyType>` or `<Potato>`, but the professional engineering standard is to use `<T>`.

When you define `function getFirst<T>(...)`, you are telling the TypeScript compiler: *"I do not know what the data type is yet. Create a temporary placeholder called `T`. When someone finally calls this function, look at the data they passed in, and replace every `T` with that exact type."*

### Symbol-by-Symbol Syntax Deconstruction
Let us deconstruct `function getFirst<T>(arr: T[]): T {`:

* `function` -> Keyword initiating a function machine.
* `getFirst` -> The developer-invented name of the machine.
* `<` -> Opening angle bracket signaling the start of the generic type variables.
* `T` -> The developer-chosen label for the temporary type placeholder.
* `>` -> Closing angle bracket.
* `(` -> Opening parenthesis for the input parameters.
* `arr` -> The developer-chosen label for the array input.
* `:` -> Type anchor.
* `T[]` -> The type rule: "An array consisting of whatever type `T` ends up being."
* `)` -> Closing parenthesis for parameters.
* `:` -> Return type anchor.
* `T` -> The output rule: "This machine will return a single item of whatever type `T` ends up being."
* `{` -> Opening curly brace for the function body.

---

## 3. Generic Functions in Practice

You can use multiple generic type variables if a function processes independent data types. We label them alphabetically (e.g., `<A, B>` or `<T, U>`).

```typescript
// We declare TWO type variables: A and B
function swap<A, B>(first: A, second: B): [B, A] {
  // We return them in reverse order
  return [second, first];
}

// We pass a string ("hello") and a number (42).
// TypeScript instantly infers: A = string, B = number.
// The return type is strictly known as: [number, string]
let swappedPair = swap("hello", 42); 
```

---

## 4. Tuples

Before we continue, notice the return type `[B, A]` in the swap function above. This is a **Tuple**.

### The Real-World Analogy: The Fixed-Slot Toolbelt
An array (`string[]`) is like a massive bucket where you can toss 100 strings. 
A **Tuple** is a specialized toolbelt with exactly two slots. Slot 1 is rigidly molded to hold exactly one hammer (`string`), and Slot 2 is rigidly molded to hold exactly one measuring tape (`number`). You cannot put a third item in, and you cannot swap their slots.

### The Core Technical Concept
A tuple is a fixed-length array where the exact type of *each specific index position* is known in advance.

```typescript
// Defining a Tuple type
let coordinatePair: [string, number] = ["Latitude", 45.987];

// Valid
console.log(coordinatePair[0]); // TypeScript knows this is a string
console.log(coordinatePair[1]); // TypeScript knows this is a number

// coordinatePair[2] = "Extra"; // COMPILER ERROR: Tuple type '[string, number]' of length '2' has no element at index '2'.
```

Tuples are heavily used in modern frameworks (like React's `useState` hook) to return exactly two related items from a single function: a value, and a function to update that value.

---

## 5. Generic Constraints (`extends`)

### The Real-World Analogy: The Bouncer's Minimum Requirement
If you run a generic function `<T>`, the compiler assumes `T` could be absolutely anything in the universe (a string, a boolean, a `null`, an object). Because `T` could be a boolean, you cannot ask for its `.length` (booleans don't have lengths).
To fix this, you add a **Constraint** using the `extends` keyword. This is like a bouncer at the club door saying: *"I don't care who you are or what your name is (`T`), as long as you are wearing a tie (`extends { length: number }`)."*

### The Core Technical Concept
You limit what types are allowed to be passed into your generic placeholder by extending an interface.

```typescript
// We enforce that whatever T is, it MUST contain a 'length' property!
function printLength<T extends { length: number }>(item: T): void {
  // Now TypeScript allows this, because it is guaranteed to exist!
  console.log("The length is: " + item.length);
}

printLength("Hello World"); // Valid! Strings have a .length property.
printLength([1, 2, 3, 4]);  // Valid! Arrays have a .length property.

// printLength(42); // COMPILER ERROR: Type 'number' does not satisfy the constraint '{ length: number }'.
```

### Why Senior Developers Require This
When writing a generic database `updateRecord<T>(record: T)` function, it must work for `User` records, `Product` records, and `Invoice` records. But the database must know the ID to update! By writing `updateRecord<T extends { id: string }>(record: T)`, the compiler guarantees that nobody can pass an object into the database updater unless it has a valid `id` property.

---

## 6. Generic Interfaces and Default Types

### The Core Technical Concept
Just like functions, interfaces can also be Generic. You attach the `<T>` placeholder to the interface name.

```typescript
// A generic blueprint where the 'data' property can be any type!
interface ApiResponse<T> {
  success: boolean;
  data: T;
  timestamp: string;
}

// We create specific configurations of the blueprint:
type UserResponse = ApiResponse<{ name: string; age: number }>;
type NumberListResponse = ApiResponse<number[]>;
```

### Default Types (`=`)
If you want a generic to fallback to a standard type when the developer doesn't provide one, you use the equals sign `=` inside the generic brackets:

```typescript
// If no <T> is provided, T defaults to 'string'
interface PaginatedList<T = string> {
  items: T[];
  currentPage: number;
}

// We didn't specify <T>, so it defaults to strings!
const textList: PaginatedList = {
  items: ["apple", "banana"],
  currentPage: 1
};

// We override the default with a custom object
const userList: PaginatedList<{ id: string }> = {
  items: [{ id: "u-1" }],
  currentPage: 1
};
```

---

## 7. Generic Type Inference

### The Core Technical Concept
You might be wondering: *"Do I have to type out `<string>` manually every single time I call a generic function?"*
The answer is no! The TypeScript compiler features **Generic Argument Inference**. It is incredibly smart. It simply looks at the data you pass into the function parentheses, figures out what type it is, and automatically fills in the `<T>` variable for you invisibly.

```typescript
function identity<T>(value: T): T {
  return value;
}

// TypeScript looks at 42, knows it is a number, and silently sets T = number.
let inferredNumber = identity(42); 

// You ONLY write the brackets manually if TypeScript guesses wrong, 
// or if you want to be extremely strict about a Union type:
let strictUnion = identity<string | number>("hello");
```

---

## 8. Real-World Use Cases and Common Pitfalls

### Real-World Use Case 1: Reusable HTTP API Wrappers (`ApiResponse<T>`)
Every enterprise web application communicates with backend servers. Instead of writing 50 separate, repetitive interfaces for `FetchUserResponse`, `FetchProductResponse`, and `FetchOrderResponse`, architects write a single generic `ApiResponse<T>` wrapper. This guarantees that the `success` and `errorCode` properties are standardized globally across the entire company, while the `.data` payload remains strictly typed for each specific API call.

### Real-World Use Case 2: Frontend State Management Hooks (`useState<T>`)
In modern frontend frameworks like React, UI state containers use generics. When you declare `const [users, setUsers] = useState<UserProfile[]>([])`, TypeScript enforces that the UI component can only ever store arrays of strictly validated User profiles inside its memory, preventing accidental UI crashes.

### Common Pitfalls & Mix-Ups
1. **The Over-Engineering Trap (Meaningless Generics):** Beginners often sprinkle `<T>` everywhere because it looks professional. **Rule of thumb:** A generic type variable `T` is only useful if it links TWO OR MORE things together (like linking an input parameter to a return type). If `<T>` only appears exactly once in your function signature, you should just use `unknown` instead!
2. **Confusing `<T>` with JSX/HTML Tags:** In files that end with `.tsx` (React files), writing `const myFunc = <T>(value: T) => {}` confuses the compiler because it thinks `<T>` is an HTML tag (like `<div>`)! To fix this in React files, you must add a trailing comma: `const myFunc = <T,>(value: T) => {}` to prove it is a TypeScript generic.
