# Module 04 Exercise: Unions, Narrowing & Discriminated Unions

Write your solutions inside the **ANSWER HERE** blocks below.

---

### Challenge 1: Type Narrowing with `typeof` and `in`
Write a function called `formatInput` that takes a parameter `input: string | number | { title: string }`.
1. If `input` is a string, return it trimmed and in uppercase.
2. If `input` is a number, return `$${input.toFixed(2)}`.
3. If `input` is an object containing `title`, return `input.title.toUpperCase()`.

#### ✍️ ANSWER HERE:
```typescript
// Write your formatInput function here:


```

---

### Challenge 2: Custom Type Guard (`is...`)
Create two interfaces: `Car { drive(): void; wheels: number; }` and `Boat { sail(): void; anchor: boolean; }`.
1. Write a custom type guard function called `isCar(vehicle: Car | Boat): vehicle is Car`.
2. Write a function called `operateVehicle(vehicle: Car | Boat)` that uses `isCar(vehicle)` inside an `if` block to call either `.drive()` or `.sail()`.

#### ✍️ ANSWER HERE:
```typescript
// Write your interfaces, type guard, and operateVehicle function here:


```

---

### Challenge 3: Discriminated Union State Machine
Build a discriminated union representing an async network request state:
1. `NetworkState` union with 4 shapes:
   - `{ status: "idle" }`
   - `{ status: "loading" }`
   - `{ status: "success", payload: string[] }`
   - `{ status: "error", code: number, message: string }`
2. Write a exhaustive `renderNetworkState(state: NetworkState): string` function using a `switch` statement that handles all 4 states.
3. *Bonus:* Add a default case using the `never` type to ensure exhaustiveness checking at compile time!

#### ✍️ ANSWER HERE:
```typescript
// Write your NetworkState union and render function here:


```
