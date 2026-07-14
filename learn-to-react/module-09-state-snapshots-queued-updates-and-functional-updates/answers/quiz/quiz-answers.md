# Quiz Answers: State Snapshots, Queued Updates, and Functional Updates

1. **What is the central rule of this module?**

   Each render sees a state snapshot; use functional updates when the next value depends on the queued previous value.

2. **What common mistake should be avoided?**

   Do not expect a setter to change the current render variable immediately.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.