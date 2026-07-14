# Module 20: Keyboard Access, Focus, and Visible Interaction States

## What you will learn

Make every interaction reachable, operable, and understandable without a pointing device.

## Native controls already support keyboards

Use button for actions and a for navigation. Rebuilding them with div requires many easy-to-miss keyboard, focus, and accessibility behaviors.

## Focus order should follow meaning

DOM order normally determines keyboard order. Avoid positive tabindex values that create a separate, fragile sequence.

## Focus must remain visible

Provide a strong focus-visible indicator and ensure sticky headers or dialogs do not cover the focused element. Focus should move only for a clear interaction reason.

## Complete example

```html
<style>
  .skip-link {
    position: absolute;
    inset-inline-start: 1rem;
    inset-block-start: -5rem;
  }

  .skip-link:focus {
    inset-block-start: 1rem;
    padding: 0.75rem;
    background: Canvas;
    color: CanvasText;
    z-index: 10;
  }

  :focus-visible {
    outline: 0.2rem solid #d97706;
    outline-offset: 0.2rem;
  }
</style>

<a class="skip-link" href="#main-content">Skip to main content</a>
<nav aria-label="Primary"><a href="/events.html">Events</a></nav>
<main id="main-content" tabindex="-1">
  <h1>Garden events</h1>
  <button type="button">Show event details</button>
</main>
```

## Try it and inspect the result

Use only Tab, Shift+Tab, Enter, Space, and the skip link. Never use the mouse during the test.

Expected result: Focus follows source order, is always visible, the link navigates, and the button activates with native keyboard behavior.

## Common mistake

Do not add tabindex=0 to every element. Only interactive elements or deliberate composite-widget parts belong in the tab sequence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 21](../module-21-accessible-names-forms-tables-and-careful-aria/README.md).

