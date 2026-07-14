# Module 22: Custom Properties, Reusable Components, and Design Consistency

## What you will learn

Define a small visual vocabulary and reusable component classes without hiding semantic HTML.

## Custom properties name design decisions

Properties such as --space-3 or --color-accent centralize repeated values and can change by context. Names should describe purpose more often than a temporary literal color.

## Components combine structure and style

A card or button class should have a clear responsibility and usable default. Variants add one explicit difference instead of copying the whole rule set.

## Consistency needs boundaries

A small scale for spacing, type, radii, and color is easier to use than dozens of nearly identical values. Accessibility constraints still override visual uniformity.

## Complete example

```html
<style>
  :root {
    --color-accent: #285f2a;
    --color-on-accent: #ffffff;
    --space-2: 0.5rem;
    --space-3: 1rem;
    --radius: 0.4rem;
  }

  .button {
    display: inline-block;
    padding: var(--space-2) var(--space-3);
    border: 0.125rem solid var(--color-accent);
    border-radius: var(--radius);
    background: var(--color-accent);
    color: var(--color-on-accent);
    font: inherit;
  }

  .button--quiet {
    background: transparent;
    color: var(--color-accent);
  }
</style>

<button class="button" type="button">Join workshop</button>
<button class="button button--quiet" type="button">Cancel</button>
```

## Try it and inspect the result

Change the accent property once, then verify both variants, hover, focus, disabled, zoom, and contrast behavior.

Expected result: Shared decisions come from named properties and one base class, while the quiet variant changes only its intended difference.

## Common mistake

Do not turn every one-off value into a global token. Name repeated decisions that have stable meaning.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 23](../module-23-transforms-transitions-animation-and-reduced-motion/README.md).

