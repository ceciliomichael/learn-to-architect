# Module 03: Working with Text and Numbers

## Before you start

Complete Modules 01 and 02. You should know strings, numbers, variables, and `console.log`.

## What you will learn

- combine and inspect strings
- use template strings to insert values into text
- perform arithmetic and understand calculation order
- round numbers for display
- recognize `NaN` as an invalid numeric result

## Why this matters

Many programs calculate totals and turn stored information into messages. These are small operations, but they appear everywhere.

## 1. Join strings with `+`

The `+` operator joins strings:

```typescript
const firstName = "Ari";
const greeting = "Hello, " + firstName + "!";

console.log(greeting);
```

Expected output:

```text
Hello, Ari!
```

Spacing inside the strings matters. Without the space after the comma, the name would touch the comma.

## 2. Use template strings for readable messages

A template string uses backticks instead of quotation marks. A placeholder begins with `${` and ends with `}`.

```typescript
const item = "notebook";
const price = 80;
const message = `The ${item} costs ${price} pesos.`;

console.log(message);
```

The placeholder is replaced with the value of the named variable.

Use a template string when a message contains several values. It is usually easier to read than a long chain of `+` operators.

## 3. Useful string information and methods

A property describes a value. A method performs an action connected to a value.

```typescript
const topic = "TypeScript";

console.log(topic.length);
console.log(topic.toUpperCase());
console.log(topic.toLowerCase());
```

Expected output:

```text
10
TYPESCRIPT
typescript
```

`length` is a property, so it has no parentheses. `toUpperCase` and `toLowerCase` are methods, so calling them uses parentheses.

These methods return new strings. They do not change the original string:

```typescript
const word = "calm";
const loudWord = word.toUpperCase();

console.log(word);
console.log(loudWord);
```

## 4. Arithmetic operators

```typescript
const addition = 8 + 2;
const subtraction = 8 - 2;
const multiplication = 8 * 2;
const division = 8 / 2;
const remainder = 8 % 3;

console.log(addition);
console.log(subtraction);
console.log(multiplication);
console.log(division);
console.log(remainder);
```

`%` gives the remainder after division. `8 % 3` is `2` because 3 fits into 8 twice with 2 left.

## 5. Calculation order

Multiplication and division happen before addition and subtraction:

```typescript
const result = 2 + 3 * 4;
console.log(result);
```

The result is `14`, not `20`.

Use parentheses to make a different order clear:

```typescript
const groupedResult = (2 + 3) * 4;
console.log(groupedResult);
```

The result is `20`.

## 6. Update a number

```typescript
let points = 10;
points = points + 5;

console.log(points);
```

The right side is calculated first. Then the result is assigned back to `points`.

The shorter form is:

```typescript
points += 5;
```

You can also use `-=`, `*=`, and `/=`. The longer form is often clearer while you are learning.

## 7. Decimal numbers and rounding

JavaScript uses one main `number` type for whole numbers and decimal numbers.

```typescript
const average = 17 / 3;

console.log(average);
console.log(Math.round(average));
console.log(average.toFixed(2));
```

`Math.round` returns the nearest whole number. `toFixed(2)` returns a string with two digits after the decimal point. It is meant for display.

Decimal calculations can have tiny precision differences:

```typescript
console.log(0.1 + 0.2);
```

This commonly prints `0.30000000000000004`. It is a result of how many decimal values are represented in binary. Later applications should use rules suitable for their domain, especially for money.

## 8. `NaN` means an invalid numeric result

`NaN` stands for Not a Number, but its JavaScript type is still `number`.

```typescript
const invalidResult = 0 / 0;

console.log(invalidResult);
console.log(typeof invalidResult);
console.log(Number.isNaN(invalidResult));
```

Expected output:

```text
NaN
number
true
```

Use `Number.isNaN` when you need to check for this special value.

## Predict the result

```typescript
const name = "Nia";
const completed = 3;
const total = 5;
const remaining = total - completed;

console.log(`${name} has ${remaining} lessons left.`);
console.log((completed + 1) * 2);
```

## Common mistakes

### Using quotation marks instead of backticks

`${name}` is replaced only inside a template string made with backticks.

### Calling `.length()`

String length is a property. Write `text.length`, not `text.length()`.

### Expecting `toUpperCase` to change the original

Store the returned string if you want to use it later.

### Mixing strings and numbers with `+`

If either side is a string, `+` may join text instead of adding numbers. Keep numeric data as numbers.

## Check your understanding

1. What is the difference between quotation marks and backticks in these examples?
2. Does `toUpperCase` change the original string?
3. What does `%` calculate?
4. Why does `(2 + 3) * 4` differ from `2 + 3 * 4`?
5. What type of value does `toFixed` return?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 04](../04-comparisons-and-decisions/README.md) uses calculated boolean values to make choices.
