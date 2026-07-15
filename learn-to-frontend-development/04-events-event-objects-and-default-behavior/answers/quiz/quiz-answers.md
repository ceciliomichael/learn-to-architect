# Quiz Answers: Events, Event Objects, and Default Behavior

1. **Why listen for submit instead of button click?**

   Submit covers keyboard submission and other native form submission paths.

2. **What is event.currentTarget?**

   The element whose listener is currently running.

3. **What is event.target?**

   The deepest dispatched target, which may be a descendant.

4. **When should preventDefault be used?**

   When code intentionally replaces a cancelable native behavior.

5. **Does preventDefault stop propagation?**

   No. Cancellation and propagation are separate.

