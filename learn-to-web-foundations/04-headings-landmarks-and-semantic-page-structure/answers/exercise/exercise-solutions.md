# Exercise Solution: Headings, Landmarks, and Semantic Page Structure

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>City Garden</title>
  </head>
  <body>
    <header>
      <p>City Garden</p>
      <nav aria-label="Primary">
        <a href="/">Home</a>
        <a href="/events.html">Events</a>
      </nav>
    </header>
    <main>
      <h1>Welcome to City Garden</h1>
      <section>
        <h2>This week's work</h2>
        <p>We are preparing the seed beds.</p>
      </section>
    </main>
    <footer><p>Open to all neighbors.</p></footer>
  </body>
</html>
```

## Why this works

The document has a primary navigation landmark, one main region, and headings that express the content hierarchy. Use the browser inspector to connect each exercise requirement to the exact element, attribute, rule, request, or computed value that satisfies it. File names and content may differ when the same semantic and accessibility contracts are preserved.

