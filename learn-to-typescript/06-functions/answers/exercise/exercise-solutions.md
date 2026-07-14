# Module 06 Exercise Solutions

## Warm-up solution

```typescript
function greetLearner(name: string) {
  console.log(`Hello, ${name}. Keep going!`);
}

greetLearner("Amir");
greetLearner("Bea");
greetLearner("Chen");
```

Each argument becomes the local value of `name` during that call.

## Guided exercise solution

```typescript
function convertHoursToMinutes(hours: number) {
  return hours * 60;
}

const hours = 2;
const minutes = convertHoursToMinutes(hours);

console.log(`${hours} hours is ${minutes} minutes.`);
```

The function returns a number. The caller stores that result and decides how to display it.

## Independent exercise solution

```typescript
function calculateDiscountedPrice(price: number, discountPercent: number) {
  const discountAmount = price * (discountPercent / 100);
  return price - discountAmount;
}

console.log(calculateDiscountedPrice(1000, 15));
console.log(calculateDiscountedPrice(500, 20));
```

Expected output:

```text
850
400
```

An alternative calculation is `price * (1 - discountPercent / 100)`. Both follow the same math. The longer version names the intermediate meaning and may be easier to inspect.

## Decision exercise solution

```typescript
function isWithinRange(value: number, minimum: number, maximum: number) {
  return value >= minimum && value <= maximum;
}

console.log(isWithinRange(5, 1, 10));
console.log(isWithinRange(12, 1, 10));
```

The returned boolean is the result of both comparisons.

## Debugging task solution

```typescript
function addNumbers(left: number, right: number) {
  const result = left + right;
  return result;
}

const answer = addNumbers(7, 8);
console.log(answer);
```

The original function printed its local result but did not return it. A function with no returned value gives the caller `undefined`. Returning `result` lets `answer` receive `15`.
