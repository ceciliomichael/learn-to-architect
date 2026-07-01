# Challenge 03: Solution

```typescript
type Result<T> =
  | { success: true;  data: T }
  | { success: false; error: string };

function divideNumbers(a: number, b: number): Result<number> {
  if (b === 0) {
    return { success: false, error: "Cannot divide by zero." };
  }
  return { success: true, data: a / b };
}

function parseAge(input: string): Result<number> {
  const age = parseInt(input);
  if (isNaN(age)) {
    return { success: false, error: "Not a valid number." };
  }
  if (age < 1 || age > 120) {
    return { success: false, error: "Age must be between 1 and 120." };
  }
  return { success: true, data: age };
}

// Test divideNumbers:
const divResult1 = divideNumbers(10, 2);
if (divResult1.success) {
  console.log("10 / 2 =", divResult1.data); // 5
} else {
  console.log("Error:", divResult1.error);
}

const divResult2 = divideNumbers(5, 0);
if (divResult2.success) {
  console.log("Result:", divResult2.data);
} else {
  console.log("Error:", divResult2.error); // "Cannot divide by zero."
}

// Test parseAge:
const ageResult1 = parseAge("25");
if (ageResult1.success) {
  console.log("Age:", ageResult1.data); // 25
} else {
  console.log("Error:", ageResult1.error);
}

const ageResult2 = parseAge("not-a-number");
if (ageResult2.success) {
  console.log("Age:", ageResult2.data);
} else {
  console.log("Error:", ageResult2.error); // "Not a valid number."
}
```
