# Challenge 02: Solution

```typescript
interface AppConfig {
  theme: "light" | "dark";
  language: string;
  maxRetries: number;
}

function getConfigValue<K extends keyof AppConfig>(config: AppConfig, key: K): AppConfig[K] {
  return config[key];
}

const config: AppConfig = {
  theme: "dark",
  language: "en",
  maxRetries: 3
};

const theme   = getConfigValue(config, "theme");      // Return type: "light" | "dark"
const retries = getConfigValue(config, "maxRetries"); // Return type: number

console.log(theme);   // "dark"
console.log(retries); // 3

// getConfigValue(config, "color");
// ERROR: Argument of type '"color"' is not assignable to parameter of type 'keyof AppConfig'.
```
