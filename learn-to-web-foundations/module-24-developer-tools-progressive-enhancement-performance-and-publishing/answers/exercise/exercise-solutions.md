# Exercise Solution: Developer Tools, Progressive Enhancement, Performance, and Publishing

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="Events and opening hours for City Garden.">
    <link rel="stylesheet" href="styles.css">
    <title>City Garden</title>
  </head>
  <body>
    <a href="#main">Skip to main content</a>
    <header>
      <nav aria-label="Primary">
        <a href="index.html" aria-current="page">Home</a>
        <a href="events.html">Events</a>
      </nav>
    </header>
    <main id="main">
      <h1>City Garden</h1>
      <p>Grow food and learn with your neighbors.</p>
    </main>
    <footer><p>Contact: garden@example.test</p></footer>
  </body>
</html>
```

## Why this works

Core content and navigation work without CSS, enhanced styling loads from a valid path, and publishing checks use browser evidence. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

