# Challenge 03: Record and typeof

Practice two of the most practical utility tools in TypeScript.

## Your Tasks

**Part 1  -  `Record`:**
Create a type alias `HttpStatusMap` using `Record<string, number>`. Create a variable `statusCodes: HttpStatusMap` containing at least 5 real HTTP status codes (e.g. `ok: 200`, `notFound: 404`, `internalServerError: 500`). Log the value of two status codes.

**Part 2  -  `typeof` in the type system:**
You have this runtime constant (do not change it)
```typescript
const defaultTheme = {
  primaryColor: "#6366f1",
  backgroundColor: "#ffffff",
  fontSize: 16,
  borderRadius: 8,
  darkMode: false
};
```

1. Use `typeof` to extract the type of `defaultTheme` as a type alias `ThemeConfig`.
2. Create a variable `partialTheme: Partial<ThemeConfig>` that overrides only `primaryColor` and `darkMode`.
3. Log both overridden properties.

## ANSWER HERE

```typescript
// Part 1
// Part 2
const defaultTheme = {
  primaryColor: "#6366f1",
  backgroundColor: "#ffffff",
  fontSize: 16,
  borderRadius: 8,
  darkMode: false
};


```
