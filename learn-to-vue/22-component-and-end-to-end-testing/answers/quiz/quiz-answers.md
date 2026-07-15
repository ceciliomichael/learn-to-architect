# Quiz Answers: Component and End-to-End Testing

1. **What is the central rule of this module?**

   Component tests assert visible behavior through accessible queries, and end-to-end tests exercise critical browser flows against controlled data.

2. **What common mistake should be avoided?**

   Do not test private component variables or build an end-to-end suite around arbitrary waits and shared mutable accounts.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.