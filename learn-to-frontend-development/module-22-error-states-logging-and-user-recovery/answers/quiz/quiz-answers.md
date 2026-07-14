# Quiz Answers: Error States, Logging, and User Recovery

1. **What should a user-facing error explain?**

   What failed in user terms and what safe recovery is available.

2. **What belongs in technical logs?**

   Useful context and correlation identifiers without secrets or unnecessary personal data.

3. **Why provide retry ownership?**

   Retries need limits, cancellation, duplicate-action protection, and a clear triggering user.

4. **Should all errors use the same message?**

   No. Expected empty, validation, offline, unauthorized, and server failures need distinct actions.

5. **Why preserve user input?**

   Recoverable failure should not force users to repeat valid work.

