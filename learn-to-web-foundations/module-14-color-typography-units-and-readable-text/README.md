# Module 14: Color, Typography, Units, and Readable Text

## What you will learn

Create readable text that respects user settings, supports zoom, and maintains sufficient contrast.

## Typography establishes a readable rhythm

Choose a dependable font stack, comfortable line height, restrained line length, and a visible hierarchy. Body text should remain readable without zoom.

## Relative units adapt

rem follows the root font size, em follows the current font size, and percentages depend on the property context. Use relative units for text and spacing when user scaling should carry through.

## Color needs contrast and redundancy

Text and meaningful controls need sufficient contrast. Do not communicate status through hue alone; add text, shape, icons with names, or other cues.

## Complete example

```html
<style>
  :root {
    color-scheme: light dark;
    font-family: system-ui, sans-serif;
    line-height: 1.6;
  }

  body {
    margin: 0;
    padding: 1.5rem;
  }

  main {
    max-width: 65ch;
    margin-inline: auto;
  }

  .status {
    border-inline-start: 0.35rem solid currentColor;
    padding-inline-start: 0.75rem;
    font-weight: 700;
  }
</style>

<main>
  <h1>Workshop details</h1>
  <p class="status">Registration status: Open</p>
  <p>Bring gloves and a refillable water bottle.</p>
</main>
```

## Try it and inspect the result

Zoom text to 200 percent, switch system color scheme if supported, and inspect line length.

Expected result: Text remains readable, lines stay constrained, and status has words plus a non-color border cue.

## Common mistake

Do not use px everywhere to force text and spacing to ignore user font preferences.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 15](../module-15-normal-flow-display-and-positioning/README.md).

