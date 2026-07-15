# Quiz Answers: Loading UI, Streaming, and Suspense

1. **What is the central rule of this module?**

   A loading file and Suspense boundaries let ready parts render while slower server work continues, but each fallback must be meaningful and accessible.

2. **What common mistake should be avoided?**

   Do not add a spinner with no label or create so many boundaries that the page flashes through unrelated placeholders.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.