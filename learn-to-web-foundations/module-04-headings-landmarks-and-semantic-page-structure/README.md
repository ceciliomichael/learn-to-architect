# Module 04: Headings, Landmarks, and Semantic Page Structure

## What you will learn

Organize a page by meaning so visual users, keyboard users, assistive technology, and maintainers can understand the same structure.

## Landmarks describe major regions

header, nav, main, aside, and footer communicate common page regions. main contains the primary content and normally appears once.

## Headings form a content outline

Choose heading levels by nesting, not by preferred font size. CSS will control appearance later.

## Sections need a reason to exist

Use article for independently meaningful content and section for a named thematic group. A div is appropriate when no semantic element fits.

## Complete example

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

## Try it and inspect the result

Open the page, inspect its Elements tree, and use the browser accessibility panel if available.

Expected result: The document has a primary navigation landmark, one main region, and headings that express the content hierarchy.

## Common mistake

Do not choose h3 because it looks smaller. Skipping from h1 to h3 hides the intended hierarchy instead of styling it.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 05](../module-05-paragraphs-lists-quotations-and-code-text/README.md).

