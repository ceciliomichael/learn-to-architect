# Module 16: Flexible One-Dimensional Layouts with Flexbox

## What you will learn

Lay out a row or column of items while allowing them to grow, shrink, wrap, and align.

## Flexbox controls one main axis

flex-direction chooses the main direction. justify-content distributes along that axis and align-items handles the cross axis.

## Items have flexible sizes

flex-grow, flex-shrink, and flex-basis form the flex shorthand. min-width: 0 may be needed when a flexible item contains content that otherwise refuses to shrink.

## Wrapping preserves usable widths

flex-wrap allows items to move to another line. Source order remains the reading and keyboard order; visual reordering should not contradict it.

## Complete example

```html
<style>
  .card-list {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    padding: 0;
    list-style: none;
  }

  .card-list > li {
    flex: 1 1 16rem;
    min-width: 0;
    padding: 1rem;
    border: 0.1rem solid #667a61;
  }
</style>

<ul class="card-list">
  <li><h2>Composting</h2><p>Learn the basics.</p></li>
  <li><h2>Seed saving</h2><p>Store seeds safely.</p></li>
  <li><h2>Watering</h2><p>Use water carefully.</p></li>
</ul>
```

## Try it and inspect the result

Resize the viewport and inspect main and cross axes in the layout tool.

Expected result: Cards share wide rows, wrap before becoming too narrow, and retain logical source order.

## Common mistake

Do not use the order property to create a visual sequence that differs from keyboard and reading order.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 17](../module-17-two-dimensional-layouts-with-grid/README.md).

