# Module 03 Quiz: Functions & Signatures

Write your choices and reasoning inside the **ANSWER HERE** blocks below each question.

---

### Question 1: `void` Return Type
Look at the following function parameter type:
```typescript
function runCallback(cb: () => void) {
  cb();
}
```
If you pass an arrow function that returns a boolean (`() => true`) into `runCallback`, will TypeScript throw a compiler error? Why or why not?

#### ✍️ ANSWER HERE:
> Answer & Explanation: 

---

### Question 2: Function Overload Signatures
When defining function overloads in TypeScript:
```typescript
function process(x: number): string;
function process(x: string): number;
function process(x: any): any {
  return typeof x === "number" ? x.toString() : parseInt(x);
}
```
Can external code directly call `process(true)` because the implementation signature has `x: any`? Explain why.

#### ✍️ ANSWER HERE:
> Answer & Explanation: 

---

### Question 3: Rest Parameters (`...args`)
How do you type a rest parameter that allows a function to accept any number of numerical arguments?

A) `function sum(...numbers: number)`  
B) `function sum(...numbers: number[])`  
C) `function sum(numbers: ...number)`  
D) `function sum(...numbers: Array)`

#### ✍️ ANSWER HERE:
> Choice: 
> Explanation: 

---

### Question 4: Arrow Function Callbacks
Why is it important to explicitly define parameter types when declaring standalone arrow functions, whereas callback functions inside `.map()` or `.filter()` often don't need parameter types?

#### ✍️ ANSWER HERE:
> Explanation: 
