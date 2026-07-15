# Module 12: Selectors, States, and Maintainable Class Names

## What you will learn

Select elements with stable, understandable intent while keeping interactive states visible and avoiding fragile page-shape dependencies.

## Classes express reusable styling roles

A class selector is usually more reusable than an id selector and less coupled to document position than a long descendant chain.

## Pseudo-classes describe state or structure

Use :hover, :focus-visible, :checked, :disabled, and structural selectors deliberately. Hover cannot be the only way to reveal required actions.

## Keep specificity predictable

Prefer shallow selectors and component class names. Avoid encoding every ancestor or using ids merely to overpower earlier rules.

## Complete example

```html
<style>
  .action-link {
    color: #145da0;
    font-weight: 700;
    text-underline-offset: 0.2em;
  }

  .action-link:hover {
    text-decoration-thickness: 0.18em;
  }

  .action-link:focus-visible {
    outline: 0.2rem solid #f0a000;
    outline-offset: 0.2rem;
  }

  .action-link[aria-current="page"] {
    color: #173b17;
  }
</style>

<nav aria-label="Primary">
  <a class="action-link" href="/" aria-current="page">Home</a>
  <a class="action-link" href="/events.html">Events</a>
</nav>
```

## Try it and inspect the result

Use Tab and pointer input. Confirm focus and hover are both visible and current-page styling does not remove the link's meaning.

Expected result: One reusable class provides base styling while state selectors add visible, non-color-only cues.

## Common mistake

Do not remove outlines globally. If a default focus indicator conflicts with the design, replace it with an equally visible custom indicator.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 13](../13-the-box-model-sizing-overflow-and-spacing/README.md).

