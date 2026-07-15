# Quiz Answers: Cache Behavior and Explicit Freshness

1. **What is the central rule of this module?**

   Treat freshness as an explicit product decision. Know whether data can be reused, for how long, and what event makes it stale, then use the current cache and revalidation APIs deliberately.

2. **What common mistake should be avoided?**

   Do not assume every fetch has the same cache behavior or hide stale-data requirements behind framework defaults.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.