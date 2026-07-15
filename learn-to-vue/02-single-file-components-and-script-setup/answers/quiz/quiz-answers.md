# Quiz Answers: Single-File Components and script setup

1. **What is the central rule of this module?**

   A Single-File Component keeps one component template, logic, and scoped presentation together. script setup exposes its top-level bindings directly to that component template.

2. **What common mistake should be avoided?**

   Do not place unrelated application services in a component file or assume scoped styles can never affect child component roots.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.