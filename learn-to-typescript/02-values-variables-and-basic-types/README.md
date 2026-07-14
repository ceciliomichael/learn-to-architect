# Module 02: Values, Variables, and Basic Types

## Before you start

Complete Module 01. You should be able to run a file and print text.

## What you will learn

- what values and variables are
- how to create names with `const` and `let`
- how assignment updates a variable
- how strings, numbers, and booleans differ
- what the runtime `typeof` operator reports

## Why this matters

Programs become useful when they can remember information. A name lets later instructions refer to a value without repeating it.

## 1. Values are pieces of information

You have already used a string value:

```typescript
console.log("Hello");
```

Here are three common kinds of value:

```typescript
console.log("Ada");
console.log(36);
console.log(true);
```

- A `string` is text.
- A `number` is a numeric value used for counting or calculation.
- A `boolean` is either `true` or `false`.

The words `string`, `number`, and `boolean` are type names. A type describes the kind of value and the operations that make sense for it.

## 2. Give a value a name with `const`

```typescript
const learnerName = "Ada";
console.log(learnerName);
```

Read the first line as: create the name `learnerName` and give it the string value `"Ada"`.

- `const` creates a name that cannot be assigned a different value later.
- `learnerName` is a name chosen by the programmer.
- `=` assigns the value on the right to the name on the left.

Names should say what a value means. `learnerName` is clearer than `x`.

## 3. Use `let` when the value must change

```typescript
let pagesRead = 3;
console.log(pagesRead);

pagesRead = 4;
console.log(pagesRead);
```

Expected output:

```text
3
4
```

The second assignment does not use `let` again. The variable already exists. The line updates its value.

Use `const` by default. Use `let` when the program needs to assign a new value to the same name.

## 4. A `const` name cannot be reassigned

```typescript
const courseName = "TypeScript";

// Intentional error: a const variable cannot be assigned again.
courseName = "JavaScript";
```

TypeScript reports an error before the program runs. Removing the second assignment fixes it.

This rule is about reassigning the name. Objects have more details, which you will learn in Module 08.

## 5. Basic types protect sensible operations

TypeScript learns the type from the first value:

```typescript
let score = 10;
score = 12;
```

Both assigned values are numbers. This is allowed.

```typescript
let score = 10;

// Intentional error: score was inferred as a number.
score = "twelve";
```

The type checker reports that a string cannot be assigned to a number variable.

This check happens during development. The type itself is not a box that exists while JavaScript runs.

## 6. Boolean values answer yes or no questions

```typescript
const isReady = true;
const isComplete = false;

console.log(isReady);
console.log(isComplete);
```

Do not put quotation marks around boolean values. `false` is a boolean. `"false"` is text containing five letters.

## 7. Inspect runtime types with `typeof`

JavaScript provides the `typeof` operator:

```typescript
const title = "Beginner";
const lessonCount = 34;
const isOpen = true;

console.log(typeof title);
console.log(typeof lessonCount);
console.log(typeof isOpen);
```

Expected output:

```text
string
number
boolean
```

`typeof` runs with the program. It reports a JavaScript runtime category. Later, you will use it to check uncertain values.

## 8. Choose readable names

TypeScript names commonly use camel case. The first word begins with a lowercase letter. Later words begin with uppercase letters:

```typescript
const firstName = "Lin";
const booksFinished = 2;
const hasLibraryCard = true;
```

A name cannot contain a space. It cannot begin with a number. It can contain digits after the first character, but descriptive words are usually easier to read.

## Predict the result

```typescript
let cupsOfWater = 1;
console.log(cupsOfWater);

cupsOfWater = 2;
console.log(cupsOfWater);
console.log(typeof cupsOfWater);
```

Write down the three output lines before running the program.

## Common mistakes

### Writing `let` during an update

```typescript
let count = 1;
count = 2;
```

Create the name once, then assign to it without `let`.

### Confusing `=` with a comparison

In this module, `=` means assignment. Module 04 introduces comparison operators.

### Putting quotation marks around every value

`"42"` is text. `42` is a number. They are not interchangeable.

### Changing the type of a variable

If a variable begins as a number, keep number values in it. Use a separate name when information has a different meaning.

## Check your understanding

1. When should you choose `let` instead of `const`?
2. What type is `"true"`?
3. What does `=` do in a variable statement?
4. Why does `let total = 5; total = "five";` cause a TypeScript error?
5. Does `typeof` run before compilation only, or does it run with JavaScript?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 03](../03-working-with-text-and-numbers/README.md) teaches useful operations for text and numbers.
