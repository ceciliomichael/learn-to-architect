# Module 26: Build, Configure, Deploy, and Maintain a Browser Application

## What you will learn

Produce a reviewed browser artifact whose configuration, paths, security policy, and rollback behavior are known.

## Contracts to understand

- No. Values embedded in browser assets are available to users.
- Strict types, tests, asset paths, size, source maps, headers, configuration, and the exact built artifact.
- Root-relative assumptions may fail outside local root hosting.
- A known previous artifact and compatible server, data, and cache behavior.
- Browser dependencies execute in the user-facing trust boundary.

## Complete TypeScript example

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

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Choose [React](../../learn-to-react/README.md) or [Vue](../../learn-to-vue/README.md) in the Web Development Learning Path.

