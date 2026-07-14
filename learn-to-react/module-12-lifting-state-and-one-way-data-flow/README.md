# Module 12: Lifting State and One-Way Data Flow

## What you will learn

Move shared state to the closest common owner and pass data down with actions up.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { useState } from "react";
type SearchProps = { value: string; onChange: (value: string) => void };
function Search({ value, onChange }: SearchProps) { return <input aria-label="Search" value={value} onChange={event => onChange(event.target.value)} />; }
function Results({ query }: { query: string }) { return <p>Showing results for {query || "everything"}.</p>; }
export function SearchPage() {
  const [query, setQuery] = useState("");
  return <><Search value={query} onChange={setQuery} /><Results query={query} /></>;
}
```

## Common mistake

Do not synchronize duplicated sibling state with competing effects.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 13](../module-13-choosing-minimal-state-and-avoiding-contradictions/README.md).