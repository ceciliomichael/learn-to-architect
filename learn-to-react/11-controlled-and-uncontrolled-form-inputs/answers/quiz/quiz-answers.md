# Quiz Answers: Controlled and Uncontrolled Form Inputs

1. **What is the central rule of this module?**

   Controlled inputs receive value and onChange from React state, while uncontrolled inputs keep current value in the DOM; choose deliberately.

2. **What common mistake should be avoided?**

   Do not pass value without an update handler and accidentally freeze an editable control.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.