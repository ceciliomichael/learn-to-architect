# Exercise Solution: Build, Configure, Deploy, and Maintain a Browser Application

```ts
type PublicConfig = {
  readonly apiBaseUrl: string;
};

function parsePublicConfig(value: unknown): PublicConfig {
  if (
    typeof value !== "object" ||
    value === null ||
    !("apiBaseUrl" in value) ||
    typeof value.apiBaseUrl !== "string"
  ) throw new Error("Invalid public configuration");

  return { apiBaseUrl: new URL(value.apiBaseUrl).toString() };
}
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

