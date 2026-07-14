# Module 13: The Box Model, Sizing, Overflow, and Spacing

## What you will learn

Reason about content, padding, borders, margins, intrinsic sizes, and overflow instead of adjusting dimensions by guesswork.

## Every rendered box has layers

The content box is surrounded by padding, border, and margin. With box-sizing: border-box, a declared width includes padding and border, which is often easier to maintain.

## Prefer flexible limits

A fixed width can overflow a narrow viewport. Use width: 100% with a sensible max-width, and let content determine height unless a fixed dimension is truly required.

## Overflow reveals a constraint conflict

Text clipping or unwanted scrolling often means a child cannot shrink, a fixed size is too small, or unbroken content needs a wrapping rule. Hiding overflow can conceal content.

## Complete example

```html
<style>
  *,
  *::before,
  *::after {
    box-sizing: border-box;
  }

  .card {
    width: 100%;
    max-width: 32rem;
    margin-inline: auto;
    padding: 1.25rem;
    border: 0.125rem solid #4b6f44;
    border-radius: 0.5rem;
    overflow-wrap: anywhere;
  }
</style>

<article class="card">
  <h1>Seed exchange</h1>
  <p>Bring labeled seeds and take varieties shared by neighbors.</p>
</article>
```

## Try it and inspect the result

Inspect the card's box-model diagram at wide and narrow viewport widths.

Expected result: The card can shrink, stays capped at a readable width, includes padding in its width, and wraps unusually long text.

## Common mistake

Do not assign a fixed height to text containers merely to align cards. Enlarged text and translated content may be clipped.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 14](../module-14-color-typography-units-and-readable-text/README.md).

