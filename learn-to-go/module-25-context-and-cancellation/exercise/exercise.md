# Exercises: Context and Cancellation

1. Write a worker that returns on completion or `ctx.Done`.
2. Give it a deadline long enough to succeed.
3. Give it a deadline short enough to cancel and inspect `context.DeadlineExceeded`.
4. Propagate one incoming context through two functions.
5. Identify configuration that belongs in an explicit parameter instead of a context value.
