# Quiz Answers: Revalidation and Updating Visible Data

1. **What is the central rule of this module?**

   After a successful mutation, update or invalidate the cached view that represents the changed data so the next render tells the truth.

2. **What common mistake should be avoided?**

   Do not revalidate before the database change commits or clear unrelated cached data without a reason.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.