# Quiz Answers: Composables and Reusable Stateful Logic

1. **What is the central rule of this module?**

   A composable is a function that uses Vue reactivity to reuse stateful behavior. Each call owns its state unless a shared owner is intentionally defined.

2. **What common mistake should be avoided?**

   Do not treat every helper as a composable or perform hidden global work merely because a function name begins with use.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.