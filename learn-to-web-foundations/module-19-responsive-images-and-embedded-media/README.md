# Module 19: Responsive Images and Embedded Media

## What you will learn

Deliver media that fits its container, selects suitable source bytes, and preserves content alternatives.

## CSS keeps media inside its container

max-inline-size: 100% and block-size: auto allow an image to shrink without distorting its aspect ratio.

## Responsive sources solve different problems

srcset with sizes lets the browser choose a resolution candidate. picture selects art direction or formats when the content itself needs a different source.

## Embeds need titles and constraints

An iframe needs a meaningful title, responsive sizing, a least-privilege allow policy, and a trusted source. Loading third-party embeds has privacy and performance costs.

## Complete example

```html
<style>
  img,
  video,
  iframe {
    max-inline-size: 100%;
  }

  img,
  video {
    block-size: auto;
  }

  .map-frame {
    inline-size: 100%;
    aspect-ratio: 16 / 9;
    border: 0;
  }
</style>

<img
  src="images/garden-800.jpg"
  srcset="images/garden-480.jpg 480w,
          images/garden-800.jpg 800w,
          images/garden-1280.jpg 1280w"
  sizes="(min-width: 60rem) 50vw, 100vw"
  width="1280"
  height="853"
  alt="Paths connecting four community garden beds">
```

## Try it and inspect the result

Resize the viewport and inspect the selected image source in developer tools.

Expected result: The image never exceeds its container, preserves its ratio, reserves space, and lets the browser select an appropriate candidate.

## Common mistake

Do not use picture merely to force a particular file size when srcset and sizes describe the same image more accurately.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 20](../module-20-keyboard-access-focus-and-visible-interaction-states/README.md).

