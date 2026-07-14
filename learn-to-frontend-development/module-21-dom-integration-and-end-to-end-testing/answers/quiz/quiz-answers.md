# Quiz Answers: DOM Integration and End-to-End Testing

1. **What should DOM tests query first?**

   Roles, labels, names, and visible text that users perceive.

2. **What does an integration test cover?**

   Several units working across a boundary such as form, renderer, and DOM.

3. **What belongs in end-to-end tests?**

   A small set of critical journeys in a real browser and realistic environment.

4. **Why avoid arbitrary sleep calls?**

   They are slow and flaky; wait for a meaningful observable condition.

5. **What must tests clean up?**

   DOM, listeners, storage, network handlers, timers, and created data they own.

