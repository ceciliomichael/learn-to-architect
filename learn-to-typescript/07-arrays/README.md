# Module 07: Arrays

## Before you start

Complete Modules 01 to 06. You should understand loops and functions.

## What you will learn

- create an ordered list with an array
- describe the type of array items
- read and update an item by index
- add and remove items
- process every item with `for...of`
- handle a possibly missing index carefully

## Why this matters

Many programs work with lists: names, prices, tasks, messages, or temperatures. An array stores these values in order.

## 1. Create an array

```typescript
const colors = ["red", "green", "blue"];
console.log(colors);
```

TypeScript infers `colors` as an array of strings.

You can write the item type explicitly:

```typescript
const scores: number[] = [85, 90, 78];
const answers: boolean[] = [true, false, true];
```

Read `number[]` as array of numbers.

## 2. Indexes begin at zero

```typescript
const cities = ["Manila", "Cebu", "Davao"];

console.log(cities[0]);
console.log(cities[1]);
console.log(cities[2]);
```

The first item is at index `0`, not index `1`.

The number of items is available through `length`:

```typescript
console.log(cities.length);
```

For three items, the final valid index is `cities.length - 1`, which is `2`.

## 3. A missing index produces `undefined`

```typescript
console.log(cities[99]);
```

At runtime, this prints `undefined`. It does not automatically throw an error.

Some strict compiler settings make array access have a possible `undefined` type. You will enable and study that setting in Module 19. Even without the setting, your program should not assume an arbitrary index exists.

## 4. Update an item

```typescript
const tasks = ["read", "walk", "cook"];
tasks[1] = "stretch";

console.log(tasks);
```

The variable is a `const`, so it cannot be assigned a different array. The existing array can still be changed. Module 16 introduces readonly arrays when changes should be blocked by the type checker.

TypeScript protects the item type:

```typescript
// Intentional error: tasks is an array of strings.
tasks[0] = 42;
```

## 5. Add and remove items

```typescript
const queue: string[] = [];

queue.push("Ava");
queue.push("Ben");
console.log(queue);

const lastPerson = queue.pop();
console.log(lastPerson);
console.log(queue);
```

- `push` adds an item to the end and returns the new length.
- `pop` removes and returns the final item.
- `pop` can return `undefined` when the array is empty.

`shift` removes the first item. `unshift` adds an item at the beginning. End operations are often simpler and faster for ordinary list work.

## 6. Visit every item with `for...of`

```typescript
const fruits = ["mango", "banana", "orange"];

for (const fruit of fruits) {
  console.log(fruit);
}
```

During each repetition, `fruit` holds the next item. Use `for...of` when you need each value and do not need its index.

## 7. Calculate from a number array

```typescript
function sumNumbers(numbers: number[]) {
  let total = 0;

  for (const number of numbers) {
    total = total + number;
  }

  return total;
}

console.log(sumNumbers([4, 6, 10]));
```

The parameter type `number[]` allows any array whose items are numbers.

## 8. Copy an array with spread

```typescript
const original = [1, 2, 3];
const copy = [...original];

copy.push(4);

console.log(original);
console.log(copy);
```

Expected output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

The spread syntax `...original` places the original items into a new array. This is a shallow copy. Nested objects require more care, which you will learn after objects.

## Predict the result

```typescript
const values = [2, 4, 6];
let total = 0;

for (const value of values) {
  total = total + value;
}

console.log(values.length);
console.log(total);
console.log(values[3]);
```

## Common mistakes

### Treating index 1 as the first item

Arrays begin at index 0.

### Calling `length`

Use `items.length`, not `items.length()`.

### Assuming `pop` always returns an item

An empty array has no final item, so the result can be `undefined`.

### Using `const` as if the array were frozen

`const` prevents reassignment of the variable. It does not prevent array methods from changing the array.

## Check your understanding

1. What is the first array index?
2. How do you find the final valid index of a nonempty array?
3. What can `pop` return for an empty array?
4. When is `for...of` useful?
5. Does `const` make an array readonly?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 08](../08-objects/README.md) groups related values under named properties.
