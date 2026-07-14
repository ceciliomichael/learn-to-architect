# Quiz Answers: Async Ownership, Abort Signals, Timeouts, and Stale Results

1. **Who owns an asynchronous task?**

   The view or operation that starts it must define completion, cancellation, errors, and cleanup.

2. **Why abort the prior search?**

   Its result is obsolete and should not consume resources or overwrite newer intent.

3. **Why compare controllers before rendering?**

   Cancellation can race with completion, so identity prevents stale commits.

4. **Is AbortError normally shown as failure?**

   Not when cancellation was an expected user or lifecycle action.

5. **What should a timeout mean?**

   A documented policy that aborts or stops waiting, not proof the server stopped work.

