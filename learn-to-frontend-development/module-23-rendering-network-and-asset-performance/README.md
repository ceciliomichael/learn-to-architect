# Module 23: Rendering, Network, and Asset Performance

## What you will learn

Measure user-relevant performance before changing code and preserve correctness and accessibility.

## Contracts to understand

- A profile identifies actual bottlenecks and provides a baseline.
- Interleaving layout reads and writes so the browser repeatedly recalculates layout.
- It can reduce initial bytes but too many requests or late critical code can hurt.
- Appropriate dimensions, formats, responsive sources, alternatives, and loading priority.
- No. Use repeated representative measurements and user-facing metrics.

## Complete TypeScript example

```ts
const started = performance.now();
requestAnimationFrame(() => {
  requestAnimationFrame(() => {
    console.log(`Two paint opportunities: ${performance.now() - started}ms`);
  });
});
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 24](../module-24-accessibility-in-dynamic-interfaces/README.md).

