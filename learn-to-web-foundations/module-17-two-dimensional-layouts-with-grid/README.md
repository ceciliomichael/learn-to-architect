# Module 17: Two-Dimensional Layouts with Grid

## What you will learn

Define rows and columns together while keeping the document source meaningful.

## Grid controls two dimensions

A grid container defines tracks. fr units share remaining space, while minmax and repeat create adaptable track patterns.

## Placement can be explicit or automatic

Named areas clarify large page regions. Auto-placement is often enough for repeated cards and adapts when item counts change.

## Intrinsic minimums still matter

minmax(0, 1fr) allows tracks to shrink below long minimum content. Test overflow rather than assuming equal fractions guarantee equal visible widths.

## Complete example

```html
<style>
  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 15rem), 1fr));
    gap: 1rem;
    padding: 0;
    list-style: none;
  }

  .gallery > li {
    padding: 1rem;
    background: #e8f0e5;
    color: #183018;
  }
</style>

<ul class="gallery">
  <li>Herbs</li>
  <li>Vegetables</li>
  <li>Flowers</li>
  <li>Fruit trees</li>
</ul>
```

## Try it and inspect the result

Use the Grid inspector and resize across the point where columns are added or removed.

Expected result: The grid creates as many usable columns as fit and collapses to one column without a special breakpoint.

## Common mistake

Do not use grid placement to make a visually attractive but semantically confusing reading order.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 18](../module-18-responsive-design-media-queries-and-container-queries/README.md).

