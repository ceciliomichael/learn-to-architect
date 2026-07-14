# Module 09: Forms, Labels, Buttons, and Input Types

## What you will learn

Collect information with controls that have names, labels, appropriate types, and predictable submission behavior.

## Every control needs an accessible label

Associate label for with a unique input id. Placeholder text is an example or hint, not a persistent label.

## Type communicates expected interaction

Use email, date, number, checkbox, radio, and other types when they match the value. Browsers can then provide useful keyboards and native behavior.

## Submission uses names and values

Successful controls contribute name-value pairs. A control without a name may be visible but is not included in ordinary form submission.

## Complete example

```html
<form action="/registrations" method="post">
  <div>
    <label for="full-name">Full name</label>
    <input id="full-name" name="fullName" autocomplete="name">
  </div>

  <div>
    <label for="email">Email address</label>
    <input id="email" name="email" type="email" autocomplete="email">
  </div>

  <label>
    <input name="updates" type="checkbox" value="yes">
    Send occasional garden updates
  </label>

  <button type="submit">Register for the workshop</button>
</form>
```

## Try it and inspect the result

Open the page, navigate controls using Tab, inspect their accessible names, and observe the submitted name-value pairs with a safe local endpoint or browser tools.

Expected result: The text controls have persistent labels, useful autocomplete tokens, submission names, and an explicit submit button.

## Common mistake

A button inside a form defaults to submit. State type=button for controls that should not submit.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 10](../module-10-form-grouping-native-validation-and-helpful-errors/README.md).

