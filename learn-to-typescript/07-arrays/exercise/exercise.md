# Module 07 Exercises

## Warm-up: A reading list

Create a string array with three book titles.

1. Print the first title.
2. Print the number of titles.
3. Add a fourth title with `push`.
4. Use `for...of` to print every title.

## Guided exercise: Find a total and average

Use this array:

```typescript
const temperatures = [28, 30, 29, 31, 27];
```

1. Create `total` before a loop.
2. Add every temperature with `for...of`.
3. Calculate the average with `total / temperatures.length`.
4. Print the total and average.

## Independent exercise: Count passing scores

Use this array:

```typescript
const scores = [65, 82, 49, 90, 73, 55];
```

Use a loop and an `if` statement to count scores that are at least `60`. Print the final count.

Expected output:

```text
4
```

## Function exercise: Find the largest value

Write `findLargest(numbers: number[])`. You may assume the input contains at least one number.

Start with the first item as the largest value found so far. Compare every item and return the final largest value.

Test it with `[4, 9, 2, 12, 7]`. The result should be `12`.

## Debugging task

Correct the problems:

```typescript
const names: string[] = ["Ana", "Bo"];
names.push(42);

for (const name of names) {
  console.log(names);
}

console.log(names[2].toUpperCase());
```

The final program should add the string `"Cy"`, print each name once, and safely print the uppercase third name.

## Completion checklist

- [ ] I used index 0 for the first item.
- [ ] I added and visited array items.
- [ ] I used a loop to calculate a result.
- [ ] I considered whether an index might be missing.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
