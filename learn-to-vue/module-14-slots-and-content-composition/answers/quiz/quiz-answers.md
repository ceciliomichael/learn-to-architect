# Quiz Answers: Slots and Content Composition

1. **What is the central rule of this module?**

   Slots let a parent supply content while the child owns surrounding structure, and named or scoped slots make those responsibilities explicit.

2. **What common mistake should be avoided?**

   Do not replace a simple prop with a slot or let slot content depend on private child details without a scoped-slot contract.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.