# Module 04: Props, Children, and Composition

## What you will learn

Props are readonly inputs and children supports composition without making a component know every nested use.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
type PanelProps = { title: string; children: React.ReactNode };
export function Panel({ title, children }: PanelProps) {
  return <section><h2>{title}</h2>{children}</section>;
}
```

## Common mistake

Do not copy props into state merely to edit or mirror them.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 05](../module-05-conditional-rendering/README.md).