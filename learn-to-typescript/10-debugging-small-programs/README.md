# Module 10: Debugging Small Programs

## Before you start

Complete Modules 01 to 09. This lesson uses all the basic programming ideas learned so far.

## What you will learn

- separate syntax, type, runtime, and logic problems
- read an error message in a useful order
- trace values through a program
- reduce a problem to a small example
- verify a fix instead of only removing an error

## Why this matters

Every programmer spends time debugging. Debugging is not random guessing. It is the process of gathering evidence, finding where behavior first differs from expectations, and testing one change at a time.

## 1. Four useful problem categories

### Syntax problem

The code does not follow the language grammar:

```typescript
// Intentional error: the closing parenthesis is missing.
console.log("Hello";
```

### Type problem

The syntax is valid, but the types do not fit:

```typescript
let count = 1;

// Intentional error: count expects a number.
count = "two";
```

### Runtime problem

The code passes type checking in its current settings but fails while running:

```typescript
const names = ["Ana"];
const missingName = names[5];

// This can fail at runtime if missingName is undefined.
console.log(missingName.toUpperCase());
```

Later, `noUncheckedIndexedAccess` will help the type checker reveal this risk.

### Logic problem

The program runs, but its result is wrong:

```typescript
const width = 5;
const height = 3;
const area = width + height;

console.log(area);
```

The area calculation should multiply. No language rule can know the programmer's intended formula.

## 2. Read the first useful error

An error normally includes:

- a file name
- a line and character position
- an error code
- a message explaining the mismatch

For example:

```text
index.ts:4:1 - error TS2322: Type 'string' is not assignable to type 'number'.
```

Read it as:

1. Open `index.ts`.
2. Go to line 4.
3. Look for a string being placed where a number is expected.
4. Inspect nearby lines that created or inferred the variable type.

Fix the earliest clear error first. One missing symbol can create several later messages.

## 3. State the expected behavior

Before changing code, write down:

- the input
- the expected output
- the actual output

Example:

```text
Input: [10, 20, 30]
Expected: 60
Actual: 30
```

This turns a vague report such as "it does not work" into a specific difference.

## 4. Trace changing values

Consider this incorrect total:

```typescript
const prices = [10, 20, 30];
let total = 0;

for (const price of prices) {
  total = price;
}

console.log(total);
```

Add a temporary trace:

```typescript
for (const price of prices) {
  console.log(`Before: total=${total}, price=${price}`);
  total = price;
  console.log(`After: total=${total}`);
}
```

The trace shows that each repetition replaces the total. The intended update is `total = total + price`.

Remove temporary logging after the problem is understood.

## 5. Reduce the example

If a program fails with 100 items, try the same operation with two. If a large function fails, call the smallest relevant calculation directly.

```typescript
function calculateLineTotal(price: number, quantity: number) {
  return price * quantity;
}

console.log(calculateLineTotal(10, 3));
```

A small example makes assumptions visible and produces less distracting output.

## 6. Check boundaries

Many bugs appear at edges:

- an empty array
- the first item
- the final item
- zero
- exactly equal to a threshold
- one below or above a threshold

For an age check, test `17`, `18`, and `19`, not only `25`.

## 7. Change one thing and run again

When many lines change together, you do not know which change fixed or caused the result.

Use this cycle:

1. Form one explanation.
2. Make the smallest change that tests it.
3. Run the relevant example.
4. Compare actual and expected results.
5. Keep or undo the change based on evidence.

## 8. A complete debugging example

The goal is to return the title of the first unread book:

```typescript
function findFirstUnreadTitle(books: { title: string; isRead: boolean }[]) {
  const unreadBook = books.find((book) => book.isRead);
  return unreadBook.title;
}
```

There are two problems:

1. The callback finds a read book because it returns `book.isRead` instead of `!book.isRead`.
2. `find` can return `undefined`, so the property access may fail.

A safe version is:

```typescript
function findFirstUnreadTitle(books: { title: string; isRead: boolean }[]) {
  const unreadBook = books.find((book) => !book.isRead);

  if (unreadBook === undefined) {
    return "No unread books";
  }

  return unreadBook.title;
}
```

Verify both cases: at least one unread book and no unread books.

## Common mistakes

### Changing code before defining the expected result

Write down what correct behavior means first.

### Hiding a type error without understanding it

Do not change a value to a convenient type until you understand what the data should mean.

### Testing only the happy path

Check empty, missing, exact-boundary, and failure cases.

### Leaving noisy debug output

Temporary traces are useful. Remove them once the behavior is understood.

## Check your understanding

1. How does a logic problem differ from a type problem?
2. Why should you fix the earliest useful error first?
3. What three facts make a bug report specific?
4. Why reduce a failing example?
5. Which boundary cases are useful for arrays and thresholds?

## Practice

Complete the [module exercises](./exercise/exercise.md). They bring together everything from Part 1. Then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 11](../11-type-inference-and-annotations/README.md) looks closely at how TypeScript infers and checks types.
