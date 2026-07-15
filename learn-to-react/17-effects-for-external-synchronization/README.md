# Module 17: Effects for External Synchronization

## What you will learn

Effects synchronize React state with an external system and return cleanup for subscriptions or owned resources.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { useEffect } from "react";
type Connection = { disconnect: () => void };
type RoomProps = { roomId: string; connect: (roomId: string) => Connection };
export function Room({ roomId, connect }: RoomProps) {
  useEffect(() => {
    const connection = connect(roomId);
    return () => connection.disconnect();
  }, [connect, roomId]);
  return <p>Connected to {roomId}.</p>;
}
```

## Common mistake

Do not use effects for calculations that belong during rendering or event logic.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 18](../18-removing-unnecessary-effects/README.md).