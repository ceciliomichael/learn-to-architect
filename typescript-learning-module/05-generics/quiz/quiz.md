# Module 05 Quiz: Generics & Type Variables

Write your answers inside the **ANSWER HERE** blocks below.

---

### Question 1: Why Generics over `any`?
Explain the architectural difference between these two function signatures:
```typescript
function processA(arg: any): any;
function processB<T>(arg: T): T;
```
If you pass `"hello"` into both, what does TypeScript know about the return value of each function?

#### ✍️ ANSWER HERE:
> Explanation: 

---

### Question 2: Generic Constraints
Look at this snippet:
```typescript
function getLength<T>(item: T): number {
  return item.length;
}
```
Why does TypeScript throw an error (`Property 'length' does not exist on type 'T'`), and how do you fix it using `extends`?

#### ✍️ ANSWER HERE:
> Why it errors & How to fix: 

---

### Question 3: Multiple Type Variables
Given the generic type:
```typescript
type Pair<K, V> = { key: K; value: V };
```
If you write `const p: Pair<string, number> = { key: "age", value: 30 };`, what are the explicit types of `K` and `V` for this instance? Can another instance use `Pair<boolean, string[]>`?

#### ✍️ ANSWER HERE:
> Explicit types of K & V: 
> Can another instance use different types? 

---

### Question 4: Generic Inference
When calling a generic function like `function identity<T>(arg: T): T`, why is it usually unnecessary to explicitly write `identity<number>(42)`?

#### ✍️ ANSWER HERE:
> Explanation: 
