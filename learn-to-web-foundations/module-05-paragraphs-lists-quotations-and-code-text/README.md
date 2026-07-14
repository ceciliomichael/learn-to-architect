# Module 05: Paragraphs, Lists, Quotations, and Code Text

## What you will learn

Choose text elements by meaning instead of using line breaks and bold text to imitate structure.

## Paragraphs and lists express different relationships

Use p for a paragraph, ul when order is not meaningful, and ol when sequence or rank matters. Each list item belongs in li.

## Quotations identify quoted material

blockquote contains a longer quotation and may cite a source. q marks a short inline quotation. cite identifies a creative work title, not automatically a person's name.

## Code-related elements preserve technical meaning

code identifies code, kbd identifies user input, and pre preserves whitespace for preformatted content. Combine pre and code for a multi-line code sample.

## Complete example

```html
<main>
  <h1>Planting instructions</h1>
  <p>Prepare these items:</p>
  <ul>
    <li>Seeds</li>
    <li>Compost</li>
    <li>Water</li>
  </ul>
  <h2>Steps</h2>
  <ol>
    <li>Fill the pot.</li>
    <li>Plant one seed.</li>
    <li>Water gently.</li>
  </ol>
  <p>Press <kbd>Ctrl</kbd> + <kbd>S</kbd> to save.</p>
  <pre><code>&lt;h1&gt;Seed journal&lt;/h1&gt;</code></pre>
</main>
```

## Try it and inspect the result

Place the fragment inside a complete document and inspect the list and code elements.

Expected result: Preparation items are unordered, steps are ordered, keyboard input is identified, and HTML code displays as text.

## Common mistake

Raw less-than signs inside a code example can be parsed as HTML. Escape them as &lt; when the markup itself must be displayed.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 06](../module-06-links-paths-navigation-and-download-safety/README.md).

