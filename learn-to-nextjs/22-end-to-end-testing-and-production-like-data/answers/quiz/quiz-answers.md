# Quiz Answers: End-to-End Testing and Production-Like Data

1. **What is the central rule of this module?**

   End-to-end tests exercise a built application through real user flows with controlled production-like test data and reliable cleanup.

2. **What common mistake should be avoided?**

   Do not make tests depend on shared mutable accounts, arbitrary delays, or a development-only runtime.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.