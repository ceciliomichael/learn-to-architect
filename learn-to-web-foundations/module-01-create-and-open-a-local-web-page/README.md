# Module 01: Create and Open a Local Web Page

## What you will learn

Create a small project folder, save a real HTML document, open it through a local web server, and use browser developer tools without needing programming experience.

## A website begins as files

A browser can read an HTML file directly, but a local HTTP server better matches how deployed sites load paths, modules, and resources. Keep source files in one clearly named project folder.

## HTML describes meaning

Tags mark the role of content. The browser parses the text into a document it can display and expose to assistive technology.

## Developer tools show browser evidence

The Elements panel shows the parsed document. The Console reports problems. The Network panel becomes useful when a local server requests files.

## Complete example

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>My first page</title>
  </head>
  <body>
    <h1>My first local web page</h1>
    <p>I created this document from plain text.</p>
  </body>
</html>
```

## Try it and inspect the result

Save as index.html. Open it directly, then serve the folder with an available editor extension or local static server.

Expected result: The browser tab says My first page and the page shows one heading and one paragraph.

## Common mistake

Do not save the file as index.html.txt. Turn on file extensions in the operating system so the real name is visible.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 02](../module-02-clients-servers-urls-dns-and-http/README.md).

