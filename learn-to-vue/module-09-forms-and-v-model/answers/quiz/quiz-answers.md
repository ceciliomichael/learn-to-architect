# Quiz Answers: Forms and v-model

1. **What is the central rule of this module?**

   v-model connects a form control value and its update event, but each control type still follows native HTML semantics and needs a label, validation, and an error path.

2. **What common mistake should be avoided?**

   Do not use a placeholder as the only label or assume v-model validates runtime input.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.