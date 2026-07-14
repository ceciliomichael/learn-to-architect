# Module 05 Exercise Solutions

## Warm-up solution

```typescript
for (let number = 2; number <= 10; number = number + 2) {
  console.log(number);
}
```

The counter starts at the first desired value and moves by two. The condition includes `10`.

## Guided exercise solution

```typescript
let total = 0;

for (let number = 1; number <= 10; number = number + 1) {
  total = total + number;
}

console.log(total);
```

Expected output:

```text
55
```

`total` must remain available between repetitions, so it is created before the loop.

## Independent exercise solution

```typescript
const baseNumber = 4;

for (let multiplier = 1; multiplier <= 5; multiplier = multiplier + 1) {
  const result = baseNumber * multiplier;
  console.log(`${baseNumber} x ${multiplier} = ${result}`);
}
```

`result` is created inside the loop because each repetition needs its own calculated result, and it is not used after the loop.

## While exercise solution

```typescript
let count = 5;

while (count >= 1) {
  console.log(count);
  count = count - 1;
}

console.log("Finished");
```

The count moves down toward `0`. At `0`, the condition is false.

## Debugging task solution

```typescript
let count = 1;

while (count <= 3) {
  console.log(count);
  count = count + 1;
}
```

The original code subtracted from a value that already satisfied `count <= 3`. Values such as `0`, `-1`, and `-2` also satisfy that condition, so the loop never moved toward stopping. Adding one makes the value eventually become `4`, where the condition is false.
