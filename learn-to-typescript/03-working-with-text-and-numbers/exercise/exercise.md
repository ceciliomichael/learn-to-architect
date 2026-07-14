# Module 03 Exercises

## Warm-up: Build a message

Create constants for a person's name and favorite food. Use a template string to print:

```text
Mara's favorite food is mango.
```

Use your own values.

## Guided exercise: Calculate a purchase

A notebook costs `45` and a pen costs `12`.

1. Store both prices in constants.
2. Store the number of notebooks as `2`.
3. Calculate the notebook subtotal.
4. Calculate the total including one pen.
5. Print `The total is 102 pesos.` using a template string and the calculated total.

Do not write `102` directly in the message.

## Independent exercise: Reading progress

Store:

- a book title
- total pages
- pages already read

Calculate the pages remaining. Print a sentence containing the title and remaining count. Then print the title in uppercase.

## Number investigation

Run this code:

```typescript
const result = 10 / 3;

console.log(result);
console.log(Math.round(result));
console.log(result.toFixed(2));
console.log(typeof result.toFixed(2));
```

Write one sentence explaining each output line.

## Debugging task

Correct the code so it prints `A pack of 4 tickets costs 200 pesos.`

```typescript
const ticketPrice = "50";
const ticketCount = 4;
const total = ticketPrice + ticketCount;

console.log("A pack of ${ticketCount} tickets costs ${total} pesos.");
```

## Completion checklist

- [ ] I used a template string with placeholders.
- [ ] I calculated a value instead of writing the answer directly.
- [ ] I used string properties or methods correctly.
- [ ] I can explain why `toFixed` returns a string.

Review the [exercise solutions](../answers/exercise/exercise-solutions.md) after completing the work.
