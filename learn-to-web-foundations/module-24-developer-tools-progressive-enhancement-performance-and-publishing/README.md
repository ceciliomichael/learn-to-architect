# Module 24: Developer Tools, Progressive Enhancement, Performance, and Publishing

## What you will learn

Inspect a complete static site, keep its core content resilient, measure its loading behavior, and publish only reviewed files.

## Debug from evidence

Use Elements and Computed styles for structure and cascade, Network for requests and sizes, Console for diagnostics, Accessibility for names and roles, and performance tools for measured timelines.

## Begin with a usable baseline

Semantic HTML should deliver content and navigation before optional styling or scripting. Add supported enhancements without making the core task depend on one fragile feature.

## Publishing is a release boundary

Verify paths under the real base URL, use HTTPS, set appropriate response metadata, remove secrets and temporary files, test a clean deployment, and document how to update or roll back.

## Complete example

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

## Try it and inspect the result

Serve from a clean copy, disable CSS, use keyboard navigation, inspect requests and accessibility properties, then test the exact published URL.

Expected result: Core content and navigation work without CSS, enhanced styling loads from a valid path, and publishing checks use browser evidence.

## Common mistake

Do not publish environment files, editor state, source maps containing private source, credentials, or unrelated build output merely because they are in the project folder.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue with the [Learn TypeScript course](../../learn-to-typescript/README.md) before Frontend Development with TypeScript.
