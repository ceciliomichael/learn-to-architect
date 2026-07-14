# Exercise Solution: Tracing Model Calls, Tools, Handoffs, and Usage

## Reference approach

1. Keep the contract beside the code that enforces it. State accepted input, produced output, and errors explicitly.
2. Parse external input into a validated internal value before calling the main rule.
3. Put the rule in a small function or module that can be tested without a real network or production service.
4. Place database, filesystem, queue, model, clock, or HTTP work behind a narrow boundary.
5. Make repeated execution safe through a transaction, idempotency key, checkpoint, unique constraint, or explicit rejection, according to the topic.
6. Return a stable error to the caller while recording a redacted diagnostic with a correlation identifier.
7. Test a valid case, invalid case, dependency failure, and recovery case. Add concurrency or cancellation evidence when the topic owns parallel or long-running work.

## Evidence to retain

Keep the automated test result and the smallest useful runtime artifact that proves Tracing Model Calls, Tools, Handoffs, and Usage behaves correctly in a controlled agent system with retrieval, tools, approval, evaluation, tracing, and durable execution. The solution is complete only when another learner can reproduce both the successful behavior and the controlled failure without relying on private accounts or production data.