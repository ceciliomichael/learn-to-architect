# Quiz Answers: Async Components, Loading, Error, and Empty States

1. **What is the central rule of this module?**

   Async components can delay code loading, while data work needs explicit loading, empty, error, success, cancellation, and retry behavior.

2. **What common mistake should be avoided?**

   Do not confuse a component download fallback with the data-loading state inside that component.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.