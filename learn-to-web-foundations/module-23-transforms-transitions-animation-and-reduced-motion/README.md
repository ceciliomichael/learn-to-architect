# Module 23: Transforms, Transitions, Animation, and Reduced Motion

## What you will learn

Use motion to explain state changes without blocking interaction, causing discomfort, or making essential information temporary.

## Motion needs a purpose

A transition can connect two states and an animation can direct attention, but continuous decorative motion competes with content.

## Transform and opacity are often efficient

They can avoid repeated layout work, but performance still needs measurement. Never animate focus or content so aggressively that it becomes hard to use.

## Reduced motion is part of the design

Honor prefers-reduced-motion by removing nonessential movement or replacing it with a simple state change. Do not remove the information the motion conveyed.

## Complete example

```html
<style>
  .details {
    transition: transform 180ms ease, opacity 180ms ease;
  }

  .details[hidden] {
    display: block;
    opacity: 0;
    transform: translateY(-0.5rem);
    visibility: hidden;
  }

  @media (prefers-reduced-motion: reduce) {
    .details {
      transition: none;
      transform: none;
    }
  }
</style>

<button type="button" aria-expanded="true" aria-controls="details">
  Workshop details
</button>
<div class="details" id="details">
  <p>Meet beside the greenhouse at 10:00 AM.</p>
</div>
```

## Try it and inspect the result

Toggle the hidden state manually in developer tools and emulate reduced motion. A later programming course will implement the button behavior.

Expected result: The visual transition has a no-motion alternative and the content relationship is represented in HTML.

## Common mistake

CSS cannot make this demonstration button functional by itself. Do not claim an interactive disclosure is complete until script updates hidden and aria-expanded together.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 24](../module-24-developer-tools-progressive-enhancement-performance-and-publishing/README.md).

