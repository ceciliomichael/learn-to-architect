# Module 01: Your First TypeScript Program

## Before you start

You do not need any programming knowledge for this module.

Use the TypeScript Playground or complete the local setup in the [course guide](../README.md#two-ways-to-run-the-examples).

## What you will learn

By the end of this module, you will be able to:

- explain what a program and a source file are
- run a TypeScript file
- print text with `console.log`
- use comments to leave notes for a reader
- recognize a statement and a string value

## Why this matters

A program is a list of instructions. Before learning larger ideas, you need a reliable way to give the computer one instruction and see its result.

## 1. Code is written instructions

Code is text written in a programming language. A programming language has rules about which words and punctuation have meaning.

Create a file named `index.ts`. The `.ts` ending tells tools that the file contains TypeScript.

Add this line:

```typescript
console.log("Hello, TypeScript!");
```

Run the file. You should see:

```text
Hello, TypeScript!
```

The line is a **statement**. A statement is one complete instruction.

## 2. Reading the first statement

Here is the same statement again:

```typescript
console.log("Hello, TypeScript!");
```

Read it from the outside inward:

- `console` gives us a place to display information.
- The dot selects something that belongs to `console`.
- `log` is the action that displays information.
- Parentheses contain the information given to that action.
- `"Hello, TypeScript!"` is a string. A string is text.
- The semicolon marks the end of the statement. TypeScript can often work without it, but this course uses semicolons consistently.

The words inside the quotation marks are data. TypeScript prints them without the quotation marks.

## 3. Programs run from top to bottom

Add three statements:

```typescript
console.log("First step");
console.log("Second step");
console.log("Third step");
```

The output keeps the same order:

```text
First step
Second step
Third step
```

For now, think of the computer as starting at the top and moving down one statement at a time.

## 4. Letter case and punctuation matter

Programming names are case-sensitive. This means `log` and `Log` are different names.

This works:

```typescript
console.log("Correct spelling");
```

This does not work:

```typescript
// Intentional error: console has no method named Log.
console.Log("Wrong letter case");
```

Quotation marks also need a matching partner:

```typescript
// Intentional error: the string is not closed.
console.log("Missing quotation mark);
```

An editor often underlines the place where it first notices a problem. The real cause may be a few characters earlier.

## 5. Comments are notes for people

TypeScript ignores comments when the program runs.

A single-line comment starts with `//`:

```typescript
// This line explains the next instruction.
console.log("The program still runs");
```

A block comment can cover more than one line:

```typescript
/*
  This is a longer note.
  It does not become output.
*/
console.log("Only this text is printed");
```

Use comments to explain why something is done. Do not comment every obvious line.

## 6. Source code and output are different

The source code is what you write:

```typescript
console.log("A message");
```

The output is what the running program displays:

```text
A message
```

Quotation marks, parentheses, and semicolons are part of the source code. They are not part of this output.

## Predict the result

Before running this code, write down the exact three output lines:

```typescript
console.log("Tea");
// console.log("Coffee");
console.log("Water");
console.log("Done");
```

The commented line does not run.

## Common mistakes

### Saving the file with the wrong ending

Check that the file is named `index.ts`, not `index.ts.txt`.

### Using curved quotation marks

Code needs straight quotation marks such as `"text"`. Quotation marks copied from formatted documents can be different characters.

### Running a command in the wrong folder

If a terminal says it cannot find `index.ts`, check which folder the terminal is currently using.

### Reading only the final error line

Start with the first error. Later errors may be side effects of the first one.

## Check your understanding

1. What does the `.ts` file ending tell your tools?
2. What is the difference between source code and output?
3. Does a line beginning with `//` run?
4. Why are quotation marks needed around text?
5. Does `console.Log` mean the same thing as `console.log`?

## Practice

Complete the [module exercises](./exercise/exercise.md). Type the code yourself and run it after each small change. Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 02](../02-values-variables-and-basic-types/README.md), you will give values names and update information while a program runs.
