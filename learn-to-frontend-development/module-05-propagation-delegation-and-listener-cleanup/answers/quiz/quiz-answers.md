# Quiz Answers: Propagation, Delegation, and Listener Cleanup

1. **What is event bubbling?**

   After reaching a target, many events propagate through ancestors.

2. **What is delegation?**

   One ancestor listener handles events from matching descendants.

3. **Why verify list.contains(button)?**

   closest can find an element outside the intended owned subtree in some nested contexts.

4. **How does AbortSignal help listeners?**

   Aborting the controller removes listeners registered with its signal.

5. **When is stopPropagation justified?**

   Only when the component contract truly owns and must stop that propagation, not as a default fix.

