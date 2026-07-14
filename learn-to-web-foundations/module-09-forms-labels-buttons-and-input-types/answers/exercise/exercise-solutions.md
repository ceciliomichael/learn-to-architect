# Exercise Solution: Forms, Labels, Buttons, and Input Types

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

## Why this works

The text controls have persistent labels, useful autocomplete tokens, submission names, and an explicit submit button. Use the browser inspector to connect each exercise requirement to the exact element, attribute, rule, request, or computed value that satisfies it. File names and content may differ when the same semantic and accessibility contracts are preserved.

