# Module 10: Form Grouping, Native Validation, and Helpful Errors

## What you will learn

Group related choices, express simple constraints in HTML, and provide errors that identify both the problem and the correction.

## fieldset groups a related question

Use fieldset and legend for radio groups, checkbox groups, or several controls forming one meaningful question.

## Native constraints are a first layer

required, minlength, maxlength, min, max, pattern, and type can prevent some invalid submissions. Server validation is still required because clients can be bypassed.

## Errors must be perceivable and actionable

Identify the field, state the rule, preserve valid entries, and move or announce focus carefully. Color alone must not carry the error meaning.

## Complete example

```html
<form action="/workshops" method="post">
  <fieldset>
    <legend>Choose a session</legend>
    <label>
      <input type="radio" name="session" value="morning" required>
      Morning
    </label>
    <label>
      <input type="radio" name="session" value="afternoon">
      Afternoon
    </label>
  </fieldset>

  <label for="seats">Number of seats</label>
  <input id="seats" name="seats" type="number" min="1" max="4" required>
  <p id="seats-help">Choose from 1 to 4 seats.</p>

  <button type="submit">Reserve seats</button>
</form>
```

## Try it and inspect the result

Submit the form empty, then test zero, five, and a valid value. Inspect which control receives focus and what message appears.

Expected result: The radio question has one group label, required choices are enforced by the browser, and the seat range is explicit.

## Common mistake

Client validation is a user-experience feature, not a security boundary. The receiving server must validate the same rules.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 11](../11-css-rules-the-cascade-inheritance-and-specificity/README.md).

