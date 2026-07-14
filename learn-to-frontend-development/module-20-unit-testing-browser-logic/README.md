# Module 20: Unit Testing Browser Logic

## What you will learn

Keep pure parsing and state transitions testable without launching a full browser.

## Contracts to understand

- A small behavior with controlled inputs and observable output.
- Pure logic is faster and easier to test across boundary cases.
- The behavioral rule and condition, not an implementation method name alone.
- No. Each test establishes and cleans its own state.
- No. They cannot prove integration with real DOM and browser behavior.

## Complete TypeScript example

```ts
export type State = { readonly count: number };

export function reduce(
  state: State,
  action: "increment" | "reset",
): State {
  if (action === "reset") return { count: 0 };
  return { count: state.count + 1 };
}

// Test expectations:
// reduce({ count: 2 }, "increment") equals { count: 3 }
// reduce({ count: 2 }, "reset") equals { count: 0 }
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 21](../module-21-dom-integration-and-end-to-end-testing/README.md).

