# Module 07: Images, Figures, Audio, Video, and Alternatives

## What you will learn

Provide media only when it serves the content, reserve its space, and supply an equivalent alternative for people who cannot use it.

## Alternative text communicates purpose

Useful images need concise alt text that performs the same content function. Decorative images use an empty alt value so assistive technology can ignore them.

## Dimensions reduce layout movement

Width and height attributes give the browser an aspect ratio before image bytes arrive. CSS can still make the image responsive.

## Audio and video require alternatives and control

Provide controls, captions for meaningful speech and sound, and a transcript when it improves access. Do not autoplay unexpected sound.

## Complete example

```html
<figure>
  <img
    src="images/raised-bed.jpg"
    width="800"
    height="533"
    alt="Three volunteers planting seedlings in a raised garden bed">
  <figcaption>Saturday planting session.</figcaption>
</figure>

<video controls width="640" poster="images/garden-tour-poster.jpg">
  <source src="media/garden-tour.webm" type="video/webm">
  <track
    kind="captions"
    src="media/garden-tour-en.vtt"
    srclang="en"
    label="English"
    default>
  <p><a href="media/garden-tour-transcript.html">Read the tour transcript</a>.</p>
</video>
```

## Try it and inspect the result

Use project-owned test media, confirm missing-file behavior, and inspect the image's accessible name.

Expected result: The figure has a useful equivalent, the browser reserves image space, and the video offers controls, captions, and a transcript fallback.

## Common mistake

Do not repeat a nearby caption word-for-word in alt text. Describe the image's purpose while the caption supplies surrounding context.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 08](../module-08-tables-for-tabular-data/README.md).

