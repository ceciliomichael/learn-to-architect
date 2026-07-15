# Exercise Solution: Responsive Images and Embedded Media

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

## Why this works

The image never exceeds its container, preserves its ratio, reserves space, and lets the browser select an appropriate candidate. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

