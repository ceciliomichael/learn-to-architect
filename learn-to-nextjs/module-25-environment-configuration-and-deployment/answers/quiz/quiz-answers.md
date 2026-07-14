# Quiz Answers: Environment Configuration and Deployment

1. **What is the central rule of this module?**

   Validate environment variables on the server, expose only explicitly public values, build in the deployment target, and document migrations, health checks, and rollback.

2. **What common mistake should be avoided?**

   Do not place secrets in NEXT_PUBLIC variables or assume a successful local development run proves deployability.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.