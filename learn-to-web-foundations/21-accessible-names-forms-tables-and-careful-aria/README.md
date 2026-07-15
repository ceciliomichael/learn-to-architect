# Module 21: Accessible Names, Forms, Tables, and Careful ARIA

## What you will learn

Use native semantics first, then add ARIA only when it supplies information HTML cannot express.

## Controls need names, roles, states, and values

Native elements usually provide role and behavior. Labels, button text, alt text, headings, and limited ARIA attributes contribute accessible names.

## ARIA does not add behavior

role=button does not create keyboard activation, focus, or form behavior. Prefer a real button. Incorrect ARIA can make a correct native element worse.

## Descriptions and errors supplement names

aria-describedby can associate stable help or error text. aria-invalid communicates an invalid state after validation, while the visible error explains correction.

## Complete example

```html
<form>
  <label for="member-email">Email address</label>
  <input
    id="member-email"
    name="email"
    type="email"
    aria-describedby="email-help email-error"
    aria-invalid="true"
    value="not-an-email">
  <p id="email-help">We use this only for workshop updates.</p>
  <p id="email-error">Enter an address containing a name, @, and domain.</p>
  <button type="submit">Save email address</button>
</form>
```

## Try it and inspect the result

Inspect the input accessibility properties and listen with a screen reader if available.

Expected result: The input has a label, help, invalid state, current value, and a visible correction message.

## Common mistake

Do not add role and ARIA attributes to a native control that already exposes the correct semantics unless a real missing relationship remains.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 22](../22-custom-properties-reusable-components-and-design-consistency/README.md).

