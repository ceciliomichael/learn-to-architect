# Module 11: CSS Rules, the Cascade, Inheritance, and Specificity

## What you will learn

Understand why a style wins before adding more selectors or using important declarations.

## A rule selects elements and declares properties

A stylesheet contains selectors and declaration blocks. Invalid declarations are ignored independently when possible.

## The cascade resolves competing declarations

Origin, importance, cascade layer, specificity, scope proximity, and source order participate in the result. For ordinary author rules at the same level, specificity and then source order commonly decide.

## Some properties inherit

Text color and font commonly inherit; margins and borders normally do not. Use browser computed styles to see the resolved value and its source.

## Complete example

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>CSS cascade</title>
    <style>
      body {
        color: #243024;
        font-family: system-ui, sans-serif;
      }

      .notice {
        border: 0.125rem solid #477a47;
        padding: 1rem;
      }

      .notice strong {
        color: #205c20;
      }
    </style>
  </head>
  <body>
    <p class="notice">Registration is <strong>open</strong>.</p>
  </body>
</html>
```

## Try it and inspect the result

Open developer tools, select strong, and inspect where its font and color values originate.

Expected result: The strong element inherits the body font, receives its own color, and sits inside a bordered paragraph.

## Common mistake

Do not reach for !important whenever a rule loses. Inspect the cascade and reduce conflicting selector complexity.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 12](../module-12-selectors-states-and-maintainable-class-names/README.md).

