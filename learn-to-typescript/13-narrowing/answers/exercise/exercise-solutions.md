# Module 13 Exercise Solutions

## Exercise 1

```typescript
function formatIdentifier(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase();
  }

  return value.toFixed(2);
}

console.log(formatIdentifier("ab-10"));
console.log(formatIdentifier(10));
```

## Exercise 2

```typescript
function printTitle(title: string | null): void {
  if (title === null) {
    console.log("No title");
    return;
  }

  console.log(title.toUpperCase());
}
```

After the early return, `title` can only be a string.

## Exercise 3

```typescript
function firstText(input: string | string[]): string | undefined {
  if (Array.isArray(input)) {
    return input[0];
  }

  return input;
}
```

The return type includes `undefined` because an empty input array has no index 0.

## Exercise 4

```typescript
function printMeasurement(value: number | undefined): void {
  if (value === undefined) {
    console.log("Missing measurement");
    return;
  }

  console.log(value);
}

printMeasurement(0);
printMeasurement(5);
printMeasurement(undefined);
```

The direct missing-value check keeps zero as valid data.

## Exercise 5

```typescript
type FileMessage = { fileName: string };
type TextMessage = { text: string };

function describeMessage(message: FileMessage | TextMessage): string {
  if ("fileName" in message) {
    return `File: ${message.fileName}`;
  }

  return `Text: ${message.text}`;
}
```

The property check exists at runtime and gives TypeScript evidence about the object shape.
