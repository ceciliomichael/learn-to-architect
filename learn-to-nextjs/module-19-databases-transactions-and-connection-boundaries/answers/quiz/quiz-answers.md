# Quiz Answers: Databases, Transactions, and Connection Boundaries

1. **What is the central rule of this module?**

   Keep database access on the server, use a connection strategy supported by the deployment environment, validate records at boundaries, and use transactions for changes that must succeed together.

2. **What common mistake should be avoided?**

   Do not open a new unmanaged connection for every render or split one atomic business change across unrelated requests.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.