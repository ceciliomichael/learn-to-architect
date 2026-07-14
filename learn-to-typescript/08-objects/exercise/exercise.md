# Module 08 Exercises

## Warm-up: Create a movie object

Create a `movie` object with:

- `title`, a string
- `releaseYear`, a number
- `hasWatched`, a boolean

Print a sentence using all three properties. Then change `hasWatched` and print the new value.

## Guided exercise: Product summary

Write this function:

```typescript
function printProduct(product: { name: string; price: number; inStock: boolean }) {
  // Your code here
}
```

It should print a product name and price. It should then print either `In stock` or `Out of stock` based on the boolean property.

Call it with two different object literals.

## Independent exercise: Find the total inventory value

Use this array:

```typescript
const inventory = [
  { name: "Pen", price: 12, quantity: 10 },
  { name: "Notebook", price: 45, quantity: 4 },
  { name: "Folder", price: 20, quantity: 6 },
];
```

Use a loop to calculate the total value of all stock. For each product, multiply price by quantity, then add it to a running total.

Expected total: `420`.

## Reference exercise

Predict the output, run the code, and explain it:

```typescript
const settings = { volume: 5 };
const sharedSettings = settings;
const copiedSettings = { ...settings };

sharedSettings.volume = 7;
copiedSettings.volume = 9;

console.log(settings.volume);
console.log(copiedSettings.volume);
```

## Debugging task

Correct the code:

```typescript
const user = {
  name = "Rin",
  age: "23",
};

console.log(user.Name);
user.age = 24;
```

The object should store `age` as a number and print the name and age.

## Completion checklist

- [ ] I created and read object properties.
- [ ] I updated a property with the same type.
- [ ] I processed an array of objects.
- [ ] I can explain shared references and shallow copies.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
