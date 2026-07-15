# Quiz Answers: Dynamic Segments, Search Parameters, and Typed Routes

1. **What is the central rule of this module?**

   Dynamic segment folders capture path values, search parameters represent query values, and both remain untrusted input even when TypeScript describes their shape.

2. **What common mistake should be avoided?**

   Do not use route or query values before validating their format and allowed range.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.