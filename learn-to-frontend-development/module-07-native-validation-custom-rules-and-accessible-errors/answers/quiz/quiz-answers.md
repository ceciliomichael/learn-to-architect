# Quiz Answers: Native Validation, Custom Rules, and Accessible Errors

1. **What does setCustomValidity with an empty string do?**

   It clears the custom error.

2. **Does client validation protect the server?**

   No. The server repeats every trusted rule.

3. **When should aria-invalid become true?**

   After validation determines the current value is invalid, according to the interaction policy.

4. **Why keep visible error text?**

   Users need a perceivable explanation and correction, not only a state flag.

5. **What should happen to valid fields after submission fails?**

   Preserve their values whenever safe so users correct only the problem.

