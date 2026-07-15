# Exercise Solution: Images, Figures, Audio, Video, and Alternatives

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

## Why this works

The figure has a useful equivalent, the browser reserves image space, and the video offers controls, captions, and a transcript fallback. Use the browser inspector to connect each exercise requirement to the exact element, attribute, rule, request, or computed value that satisfies it. File names and content may differ when the same semantic and accessibility contracts are preserved.

