# Module 09: Browser Modules, Package Imports, and Build Output

## What you will learn

Split source with explicit ES module imports and let a reviewed build resolve installed packages.

## Contracts to understand

- It enables module syntax, deferred execution, strict mode, and module-scoped bindings.
- Browsers and tools resolve an exact module URL rather than searching arbitrary names.
- It resolves and transforms a module graph into deployment assets according to configured rules.
- It records resolved dependency graph changes that affect executed code.
- Normally no; the manifest and lock file reproduce reviewed installation.

## Complete TypeScript example

```ts
// format-name.ts
export function formatName(value: string): string {
  return value.trim().replaceAll(/\s+/g, " ");
}

// main.ts
import { formatName } from "./format-name.js";

console.log(formatName("  Ada   Lovelace  "));
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 10](../10-urls-search-parameters-history-and-navigation/README.md).

