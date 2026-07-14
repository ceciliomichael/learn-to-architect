# Quiz Answers: Async Data, Cancellation, Loading, Empty, and Error States

1. **What is the central rule of this module?**

   Async UI needs owned cancellation plus distinct loading, empty, error, and success states, and stale results must not overwrite newer intent.

2. **What common mistake should be avoided?**

   Do not start an unowned fetch in an effect without cleanup and race handling.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.