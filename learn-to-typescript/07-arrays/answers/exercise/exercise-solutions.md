# Module 07 Exercise Solutions

## Warm-up solution

```typescript
const readingList = ["Coraline", "Matilda", "The Hobbit"];

console.log(readingList[0]);
console.log(readingList.length);

readingList.push("A Wrinkle in Time");

for (const title of readingList) {
  console.log(title);
}
```

Your titles can differ. The array should contain strings only.

## Guided exercise solution

```typescript
const temperatures = [28, 30, 29, 31, 27];
let total = 0;

for (const temperature of temperatures) {
  total = total + temperature;
}

const average = total / temperatures.length;

console.log(total);
console.log(average);
```

Expected output:

```text
145
29
```

## Independent exercise solution

```typescript
const scores = [65, 82, 49, 90, 73, 55];
let passingCount = 0;

for (const score of scores) {
  if (score >= 60) {
    passingCount = passingCount + 1;
  }
}

console.log(passingCount);
```

The counter changes only when the current score passes the condition.

## Function exercise solution

```typescript
function findLargest(numbers: number[]) {
  let largest = numbers[0];

  for (const number of numbers) {
    if (number > largest) {
      largest = number;
    }
  }

  return largest;
}

console.log(findLargest([4, 9, 2, 12, 7]));
```

This exercise assumes a nonempty array, as stated. Later strict settings can make TypeScript require proof that `numbers[0]` exists. A version for possibly empty arrays should return a result that includes `undefined` or handle the empty case explicitly.

## Debugging task solution

```typescript
const names: string[] = ["Ana", "Bo"];
names.push("Cy");

for (const name of names) {
  console.log(name);
}

const thirdName = names[2];

if (thirdName !== undefined) {
  console.log(thirdName.toUpperCase());
}
```

The array accepts strings, not numbers. Inside the loop, `name` is the current string, while `names` is the whole array. The explicit check makes the final access safe even if the data changes later.
