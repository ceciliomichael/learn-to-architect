# Exercise: Production Inference, Drift, and Fairness

Apply this module to the continuing project: a controlled agent system with retrieval, tools, approval, evaluation, tracing, and durable execution.

1. Write a short contract describing the input, output, owner, and failure behavior for Production Inference, Drift, and Fairness.
2. Implement the smallest complete change that demonstrates that contract.
3. Reject one invalid or unauthorized input at the boundary.
4. Exercise the normal path, empty path, dependency-failure path, and repeated-work path where relevant.
5. Add an automated check for the most important rule.
6. Collect one piece of runtime evidence, such as a structured log, metric, trace, query plan, inspected file, or protocol response.
7. Explain how the system recovers after interruption or partial failure.

## Success check

The change is understandable without hidden framework behavior, invalid data cannot silently cross the boundary, important failure behavior is tested, and no secret or personal data appears in source control or diagnostic output.