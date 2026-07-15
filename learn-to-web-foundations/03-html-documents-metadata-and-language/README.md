# Module 03: HTML Documents, Metadata, and Language

## What you will learn

Build a complete document whose encoding, language, title, viewport, and descriptive metadata are explicit.

## The document skeleton establishes parsing context

The doctype selects standards mode. html contains the document, head contains document metadata, and body contains page content.

## Language and encoding affect real users

Declare UTF-8 near the beginning and set the document language. Screen readers, translation tools, search systems, and spelling tools use that language information.

## Metadata should describe the actual page

A unique title identifies the page. A concise description can summarize it for search and sharing systems, although those systems decide how to display it.

## Complete example

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="Opening hours for North Street Library.">
    <title>Opening hours | North Street Library</title>
  </head>
  <body>
    <h1>Opening hours</h1>
    <p>Monday to Friday, 9:00 AM to 6:00 PM.</p>
  </body>
</html>
```

## Try it and inspect the result

Save as index.html, serve or open it, inspect the document element, and read the tab title.

Expected result: The visible content and metadata consistently describe the opening-hours page.

## Common mistake

Do not use a keyword-filled or unrelated description. Metadata should not promise content the page does not provide.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 04](../04-headings-landmarks-and-semantic-page-structure/README.md).

