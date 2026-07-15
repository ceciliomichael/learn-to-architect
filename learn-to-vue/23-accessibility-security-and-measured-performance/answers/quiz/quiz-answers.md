# Quiz Answers: Accessibility, Security, and Measured Performance

1. **What is the central rule of this module?**

   Preserve semantic HTML and focus, treat runtime content as untrusted, avoid raw HTML, measure rendering before optimizing, and keep reactive work close to its owner.

2. **What common mistake should be avoided?**

   Do not claim security from TypeScript or optimize with shallow tricks before profiling the actual problem.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.