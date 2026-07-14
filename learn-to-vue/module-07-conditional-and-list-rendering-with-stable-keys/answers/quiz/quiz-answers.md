# Quiz Answers: Conditional and List Rendering with Stable Keys

1. **What is the central rule of this module?**

   Use v-if when content should exist conditionally, v-show for frequent visibility changes, and v-for with a stable key derived from item identity.

2. **What common mistake should be avoided?**

   Do not combine filtering and list rendering on the same element or use an index key for reorderable data.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.