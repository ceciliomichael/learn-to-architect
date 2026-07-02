# Challenge 02: Safe Property Lookup with keyof

Use `keyof` to write a function that prevents invalid property access at compile time.

## Starting Interface

```typescript
interface AppConfig {
  theme: "light" | "dark";
  language: string;
  maxRetries: number;
}
```

## Your Tasks

1. Write a generic function `getConfigValue<K extends keyof AppConfig>(config: AppConfig, key: K): AppConfig[K]` that returns `config[key]`.

2. Create a `config` object of type `AppConfig`.

3. Call `getConfigValue` to retrieve `theme` and `maxRetries`. In a comment next to each call, write the TypeScript-inferred return type.

4. Write a commented-out call passing an invalid key (e.g. `"color"`) and write the error TypeScript produces.

## ANSWER HERE

```typescript
interface AppConfig {
  theme: "light" | "dark";
  language: string;
  maxRetries: number;
}

// Write your getConfigValue function and test calls here
```
