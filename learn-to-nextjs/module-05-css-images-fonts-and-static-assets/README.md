# Module 05: CSS, Images, Fonts, and Static Assets

## What you will learn

Use scoped or global CSS deliberately, next/image for sized and optimized images, next/font for controlled font loading, and public for files that truly need stable public URLs.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import Image from "next/image";
export function ProfileImage() {
  return <Image src="/profile.jpg" alt="Ada at her desk" width={320} height={240} />;
}
```

## Common mistake

Do not omit image dimensions, expose private files through public, or load application fonts through avoidable render-blocking requests.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 06](../module-06-metadata-social-images-and-document-information/README.md).