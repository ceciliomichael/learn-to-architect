# Challenge 03: Solution

```typescript
// Part 1: Record
type HttpStatusMap = Record<string, number>;

const statusCodes: HttpStatusMap = {
  ok: 200,
  created: 201,
  badRequest: 400,
  unauthorized: 401,
  notFound: 404,
  internalServerError: 500
};

console.log(statusCodes.ok);       // 200
console.log(statusCodes.notFound); // 404

// Part 2: typeof in the type system
const defaultTheme = {
  primaryColor: "#6366f1",
  backgroundColor: "#ffffff",
  fontSize: 16,
  borderRadius: 8,
  darkMode: false
};

// Extract the type of defaultTheme without writing it manually
type ThemeConfig = typeof defaultTheme;
// Resolves to: { primaryColor: string; backgroundColor: string; fontSize: number; borderRadius: number; darkMode: boolean; }

const partialTheme: Partial<ThemeConfig> = {
  primaryColor: "#ef4444",
  darkMode: true
};

console.log(partialTheme.primaryColor); // "#ef4444"
console.log(partialTheme.darkMode);     // true
```
