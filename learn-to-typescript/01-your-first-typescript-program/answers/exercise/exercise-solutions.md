# Module 01 Exercise Solutions

Your personal messages can differ from these examples. The important part is the structure and the output.

## Warm-up solution

```typescript
console.log("Hello, Mina");
console.log("I ran my first program.");
```

Expected output:

```text
Hello, Mina
I ran my first program.
```

Each call prints one line. The statements run from top to bottom.

## Guided exercise solution

```typescript
// Print the steps for making a simple sandwich.
console.log("1. Put bread on a plate.");
console.log("2. Add the filling.");
console.log("3. Close the sandwich.");
```

Expected output:

```text
1. Put bread on a plate.
2. Add the filling.
3. Close the sandwich.
```

The comment is visible in the source file, but it does not become output.

## Independent exercise solution

```typescript
// A short introduction
console.log("My name is Sam.");
console.log("I would like to visit Kyoto.");
console.log("I would like to build a study timer.");
console.log("End of introduction.");
```

Your first three messages should describe you. Four separate calls make four separate lines.

## Debugging task solution

```typescript
console.log("Starting now");
console.log("Practice makes progress");
console.log("Finished");
```

The fixes are:

1. `Console` became `console` because letter case matters.
2. The second string received its missing closing quotation mark.
3. A semicolon was added to the final statement for course consistency. TypeScript usually inserts it in this example, so the missing semicolon was not the error that stopped the program.

Expected output:

```text
Starting now
Practice makes progress
Finished
```

That final distinction matters. A good explanation separates required fixes from optional style fixes.
