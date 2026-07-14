# Module 08: Tables for Tabular Data

## What you will learn

Represent relationships between row and column headers without using tables as a general page-layout tool.

## A table is for data relationships

Use table when cells are understood by their intersection with row or column headers. Use CSS layout for page regions.

## Headers make relationships navigable

th identifies a header cell. scope=col or scope=row makes simple relationships explicit. Complex tables may require ids and headers or a simpler redesign.

## Captions identify the table

caption gives the table an accessible title. thead, tbody, and tfoot group rows for meaning and styling but do not replace header cells.

## Complete example

```html
<table>
  <caption>Garden opening hours</caption>
  <thead>
    <tr>
      <th scope="col">Day</th>
      <th scope="col">Opens</th>
      <th scope="col">Closes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Monday</th>
      <td>09:00</td>
      <td>18:00</td>
    </tr>
    <tr>
      <th scope="row">Saturday</th>
      <td>10:00</td>
      <td>16:00</td>
    </tr>
  </tbody>
</table>
```

## Try it and inspect the result

Place the table in a complete page and inspect its accessibility tree or use a screen reader table-navigation command.

Expected result: Every time cell is associated with both a day row header and an opens or closes column header.

## Common mistake

Do not leave an empty first header merely to make the grid look aligned. Give every data dimension a meaningful header.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 09](../module-09-forms-labels-buttons-and-input-types/README.md).

