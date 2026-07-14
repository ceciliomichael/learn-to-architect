# Module 18: Responsive Design, Media Queries, and Container Queries

## What you will learn

Let content adapt to available space and user preferences rather than targeting a list of named devices.

## Start from the narrow layout

A simple single-column base usually works in more environments. Add enhancements when space or capabilities allow.

## Media queries describe the viewport or preferences

Use width queries when the overall viewport matters and preference queries for reduced motion, contrast, or color scheme. Choose breakpoints where content needs them.

## Container queries describe component space

A component can respond to its own container rather than the whole viewport. Establish a query container and keep a usable fallback.

## Complete example

```html
<style>
  .event-region {
    container-type: inline-size;
  }

  .event {
    display: grid;
    gap: 0.75rem;
    padding: 1rem;
    border: 0.1rem solid #5c7355;
  }

  @container (min-width: 34rem) {
    .event {
      grid-template-columns: 2fr 1fr;
      align-items: start;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    * {
      scroll-behavior: auto;
    }
  }
</style>

<div class="event-region">
  <article class="event">
    <div><h2>Seed swap</h2><p>Bring labeled seeds.</p></div>
    <p><time datetime="2026-09-12">September 12</time></p>
  </article>
</div>
```

## Try it and inspect the result

Resize the container independently if developer tools allow, then emulate reduced motion.

Expected result: The component works as one column and gains a second column only when its own space allows.

## Common mistake

Do not choose breakpoints from popular phone names. Use the width where the actual content becomes crowded or gains useful space.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 19](../module-19-responsive-images-and-embedded-media/README.md).

