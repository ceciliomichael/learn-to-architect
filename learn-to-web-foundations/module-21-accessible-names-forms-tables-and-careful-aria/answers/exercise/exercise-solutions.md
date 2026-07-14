# Exercise Solution: Accessible Names, Forms, Tables, and Careful ARIA

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

## Why this works

The input has a label, help, invalid state, current value, and a visible correction message. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

