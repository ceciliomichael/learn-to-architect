# Module 03 Exercise Solutions

Check your solutions against the reference code below.

---

### Solution 1: Strongly Typed Calculator

```typescript
type Operation = "ADD" | "SUBTRACT" | "MULTIPLY" | "DIVIDE";

function calculate(operation: Operation, a: number, b: number): number {
  switch (operation) {
    case "ADD":
      return a + b;
    case "SUBTRACT":
      return a - b;
    case "MULTIPLY":
      return a * b;
    case "DIVIDE":
      if (b === 0) {
        throw new Error("Cannot divide by zero");
      }
      return a / b;
  }
}
```

---

### Solution 2: Optional vs Default Parameters

```typescript
function formatGreetingOptional(name: string, title?: string): string {
  if (title) {
    return `Hello ${title} ${name}`;
  }
  return `Hello ${name}`;
}

function formatGreetingDefault(name: string, title: string = "Explorer"): string {
  return `Hello ${title} ${name}`;
}

// formatGreetingDefault("Alice", undefined) returns "Hello Explorer Alice"
```

---

### Solution 3: Function Overloads

```typescript
// Overload Signatures (what callers see)
function parseCoordinate(x: number, y: number): { x: number; y: number };
function parseCoordinate(coordString: string): { x: number; y: number };

// Implementation Signature (what handles all runtime cases)
function parseCoordinate(arg1: number | string, arg2?: number): { x: number; y: number } {
  if (typeof arg1 === "string") {
    const [xStr, yStr] = arg1.split(",");
    return {
      x: parseFloat(xStr),
      y: parseFloat(yStr)
    };
  } else {
    return {
      x: arg1,
      y: arg2 ?? 0
    };
  }
}
```
