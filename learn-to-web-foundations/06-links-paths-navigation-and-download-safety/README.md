# Module 06: Links, Paths, Navigation, and Download Safety

## What you will learn

Connect documents with understandable link text, predictable paths, and safe behavior for new tabs and downloads.

## A link needs a destination and a purpose

The href value identifies the destination. Link text should make sense out of context and should not rely on vague phrases such as click here.

## Relative paths depend on the current document

A sibling file uses its name, a child uses folder/name, and a parent begins with ../. Root-relative paths depend on how the site is hosted.

## New contexts and downloads need care

Opening a new tab can disorient users and should be announced when unexpected. The download attribute is only a hint and does not make an untrusted file safe.

## Complete example

```html
<nav aria-label="Primary">
  <a href="index.html" aria-current="page">Home</a>
  <a href="events/index.html">Garden events</a>
  <a href="contact.html">Contact the garden team</a>
</nav>

<p>
  Read the
  <a href="documents/visitor-guide.pdf">visitor guide (PDF)</a>.
</p>

<p>
  <a href="#opening-hours">Skip to opening hours</a>
</p>
<h2 id="opening-hours">Opening hours</h2>
```

## Try it and inspect the result

Use this fragment in a project containing the named files, then test every link with keyboard and mouse navigation.

Expected result: Links reveal their destination or purpose, the current page is exposed, and the fragment link moves to a unique id.

## Common mistake

Do not use target=_blank everywhere. Preserve normal browser navigation unless a new context solves a specific user need.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 07](../07-images-figures-audio-video-and-alternatives/README.md).

