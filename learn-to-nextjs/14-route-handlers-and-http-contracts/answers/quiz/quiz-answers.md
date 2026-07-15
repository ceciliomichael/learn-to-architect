# Quiz Answers: Route Handlers and HTTP Contracts

1. **What is the central rule of this module?**

   A route handler implements an HTTP contract with Web Request and Response APIs. Parse input, validate it, enforce access, choose status codes, and return a stable response shape.

2. **What common mistake should be avoided?**

   Do not make route handlers thin unsafe tunnels to a database or external service.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.