# Module 20 Exercise Solutions

## Exercise 1

```typescript
function formatUnknown(value: unknown): string {
  if (typeof value === "string") {
    return value.toUpperCase();
  }

  if (typeof value === "number") {
    return value.toFixed(2);
  }

  return "Unsupported value";
}
```

## Exercise 2

```typescript
type UnknownRecord = { [key: string]: unknown };

interface Settings {
  theme: "light" | "dark";
  fontSize: number;
}

function isUnknownRecord(value: unknown): value is UnknownRecord {
  return typeof value === "object" && value !== null && !Array.isArray(value);
}

function isSettings(value: unknown): value is Settings {
  if (!isUnknownRecord(value)) {
    return false;
  }

  const theme = value["theme"];
  const hasValidTheme = theme === "light" || theme === "dark";

  return hasValidTheme && typeof value["fontSize"] === "number";
}
```

## Exercise 3

```typescript
function isNumberArray(value: unknown): value is number[] {
  return Array.isArray(value) && value.every((item) => typeof item === "number");
}
```

## Exercise 4

```typescript
const validValue: unknown = JSON.parse(validJson);
const invalidValue: unknown = JSON.parse(invalidJson);

console.log(isSettings(validValue));
console.log(isSettings(invalidValue));
```

The expected output is `true` followed by `false`.

## Exercise 5

`JSON.parse` produces a runtime object whose `theme` value is a number. The assertion emits no check and changes no data. The later string method call therefore fails at runtime.
