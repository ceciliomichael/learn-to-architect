# Module 02 Exercise: Objects, Interfaces & Type Aliases

Complete your solutions directly inside the **ANSWER HERE** sections below.

---

### Challenge 1: Designing an E-Commerce Cart Blueprint
Write an `interface` called `CartItem` that meets the following strict requirements:
1. `id`: A unique identifier that can NEVER be modified after creation (`readonly`).
2. `title`: The name of the item (string).
3. `price`: The price in dollars (number).
4. `discountCode`: An optional string property. If not provided, it should still be a valid `CartItem`.
5. `tags`: A list of strings (e.g., `["electronics", "sale"]`).

Now, create a valid object `myCartItem` using this interface. Then, write a line trying to change `id` and note the error.

#### ✍️ ANSWER HERE:
```typescript
// Write your CartItem interface and object here:


```

---

### Challenge 2: Index Signatures for Dynamic Configurations
Imagine you are building a language translation dictionary. You don't know what words will be added ahead of time, but you know every word key will be a string, and its translation value will also be a string.

1. Write an `interface` called `Dictionary` using an index signature.
2. Create a variable `frenchDict: Dictionary` and assign at least 3 English-to-French word pairs.
3. Try adding `wordCount: 100` to `frenchDict`. Explain why TypeScript rejects it.

#### ✍️ ANSWER HERE:
```typescript
// Write your Dictionary interface and frenchDict variable here:


```

---

### Challenge 3: Type vs. Interface Extension
You are building an application for a zoo.
1. Create an `interface` called `Animal` with `name: string` and `age: number`.
2. Create an `interface` called `Bird` that extends `Animal` and adds `canFly: boolean`.
3. Now do the exact same thing using `type` aliases (`TypeAnimal` and `TypeBird`) using intersection (`&`).

#### ✍️ ANSWER HERE:
```typescript
// Write your interface extension and type intersection here:


```
