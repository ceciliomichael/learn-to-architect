# Quiz Answers: Server and Client Component Boundaries

1. **What is the central rule of this module?**

   Components in the App Router are Server Components unless a client boundary is declared. Add use client only where browser state, effects, event handlers, or browser APIs are required.

2. **What common mistake should be avoided?**

   Do not place use client on a whole route tree just because one small button is interactive.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.