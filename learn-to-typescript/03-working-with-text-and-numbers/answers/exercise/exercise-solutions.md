# Module 03 Exercise Solutions

## Warm-up solution

```typescript
const personName = "Mara";
const favoriteFood = "mango";

console.log(`${personName}'s favorite food is ${favoriteFood}.`);
```

The apostrophe is ordinary text inside the template string.

## Guided exercise solution

```typescript
const notebookPrice = 45;
const penPrice = 12;
const notebookCount = 2;

const notebookSubtotal = notebookPrice * notebookCount;
const total = notebookSubtotal + penPrice;

console.log(`The total is ${total} pesos.`);
```

Expected output:

```text
The total is 102 pesos.
```

The total comes from the earlier values. If a price changes, the message changes without editing the answer manually.

## Independent exercise solution

```typescript
const bookTitle = "The Little Prince";
const totalPages = 96;
const pagesRead = 35;
const pagesRemaining = totalPages - pagesRead;

console.log(`${bookTitle} has ${pagesRemaining} pages remaining.`);
console.log(bookTitle.toUpperCase());
```

Expected output:

```text
The Little Prince has 61 pages remaining.
THE LITTLE PRINCE
```

## Number investigation explanation

The approximate output is:

```text
3.3333333333333335
3
3.33
string
```

1. Division produces a decimal number.
2. `Math.round` returns the nearest whole number.
3. `toFixed(2)` formats the result with two digits after the decimal point.
4. The formatted value is a string because it is prepared as text for display.

## Debugging task solution

```typescript
const ticketPrice = 50;
const ticketCount = 4;
const total = ticketPrice * ticketCount;

console.log(`A pack of ${ticketCount} tickets costs ${total} pesos.`);
```

The price must be a number for multiplication. The total uses `*`, not `+`. The message uses backticks so its placeholders are replaced.
