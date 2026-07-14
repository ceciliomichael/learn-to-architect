# Module 15: Normal Flow, Display, and Positioning

## What you will learn

Use normal document flow first, then choose display and positioning only when the relationship requires them.

## Normal flow is resilient

Block content stacks and inline content flows within lines. This default adapts naturally to unknown content and viewport sizes.

## Display changes formatting behavior

block, inline, inline-block, flex, grid, and none create different layout participation. display: none removes content from visual and accessibility rendering.

## Positioning changes reference relationships

Relative positioning preserves the original space. Absolute positioning is removed from normal flow and uses a containing block. Fixed and sticky behavior require careful overlap and zoom testing.

## Complete example

```html
<style>
  .notice {
    position: relative;
    padding: 1rem 1rem 1rem 3rem;
    border: 0.1rem solid #5e7758;
  }

  .notice__mark {
    position: absolute;
    inset-block-start: 1rem;
    inset-inline-start: 1rem;
  }
</style>

<aside class="notice" aria-labelledby="notice-title">
  <span class="notice__mark" aria-hidden="true">i</span>
  <h2 id="notice-title">Weather notice</h2>
  <p>The outdoor session moves inside when heavy rain begins.</p>
</aside>
```

## Try it and inspect the result

Increase the text size and narrow the viewport. Inspect which box establishes the absolute-positioning reference.

Expected result: The aside remains in normal flow while only its decorative mark is positioned relative to it.

## Common mistake

Do not absolutely position the main content to make a screenshot match. Unknown text length will cause overlap.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 16](../module-16-flexible-one-dimensional-layouts-with-flexbox/README.md).

