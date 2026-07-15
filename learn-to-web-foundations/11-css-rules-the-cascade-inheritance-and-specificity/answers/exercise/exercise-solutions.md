# Exercise Solution: CSS Rules, the Cascade, Inheritance, and Specificity

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

## Why this works

The strong element inherits the body font, receives its own color, and sits inside a bordered paragraph. Use the browser inspector to connect each exercise requirement to the exact element, attribute, rule, request, or computed value that satisfies it. File names and content may differ when the same semantic and accessibility contracts are preserved.

