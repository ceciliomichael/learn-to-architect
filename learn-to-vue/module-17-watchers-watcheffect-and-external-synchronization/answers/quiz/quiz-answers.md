# Quiz Answers: Watchers, watchEffect, and External Synchronization

1. **What is the central rule of this module?**

   Use watch for a chosen reactive source and watchEffect for automatically tracked synchronization. Invalidate or clean up stale asynchronous work whenever dependencies change.

2. **What common mistake should be avoided?**

   Do not use watchers for values that computed can derive or allow an older request to overwrite a newer result.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.