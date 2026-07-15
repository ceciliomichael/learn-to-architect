# Quiz Answers: Timers, Animation Frames, and Observer APIs

1. **Are timer delays exact schedules?**

   No. They are minimum delays affected by task queues, throttling, and page state.

2. **When use requestAnimationFrame?**

   For visual updates synchronized with a future paint.

3. **What does IntersectionObserver avoid?**

   Repeated manual geometry polling for visibility intersections.

4. **Who clears a timer?**

   The component or view that created and owns it.

5. **Why avoid heavy work in frequent callbacks?**

   It delays input, rendering, and other tasks.

