# Module 02: The DOM Tree and Safe Element Queries

## What you will learn

Read the parsed document as typed nodes and handle a missing or wrong element instead of asserting it away.

## Contracts to understand

- The browser's current parsed document tree, which may differ from the original source after parsing or updates.
- No element may match at the time and root being queried.
- A matching selector does not by itself prove the concrete element API expected by the code.
- When querying a document for one known id and handling its HTMLElement or null result.
- It suppresses evidence without checking runtime identity.

## Complete TypeScript example

```ts
function requireElement<T extends Element>(
  selector: string,
  expected: { new (...args: never[]): T },
): T {
  const element = document.querySelector(selector);
  if (!(element instanceof expected)) {
    throw new Error(`Expected ${selector}`);
  }
  return element;
}

const heading = requireElement("#page-title", HTMLHeadingElement);
console.log(heading.textContent);
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 03](../module-03-create-update-move-and-remove-content/README.md).

