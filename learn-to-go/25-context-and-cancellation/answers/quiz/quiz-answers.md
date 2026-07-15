# Quiz Answers: Context and Cancellation

1. First, named `ctx`.
2. It releases resources associated with the derived context promptly.
3. No. Work must cooperate by observing cancellation or using context-aware APIs.
4. No. Use explicit typed parameters or configuration.
5. Parent cancellation and deadlines then reach all descendant work.
