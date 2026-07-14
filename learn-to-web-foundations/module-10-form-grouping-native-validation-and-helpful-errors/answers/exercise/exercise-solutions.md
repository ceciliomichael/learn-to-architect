# Exercise Solution: Form Grouping, Native Validation, and Helpful Errors

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

## Why this works

The radio question has one group label, required choices are enforced by the browser, and the seat range is explicit. Use the browser inspector to connect each exercise requirement to the exact element, attribute, rule, request, or computed value that satisfies it. File names and content may differ when the same semantic and accessibility contracts are preserved.

