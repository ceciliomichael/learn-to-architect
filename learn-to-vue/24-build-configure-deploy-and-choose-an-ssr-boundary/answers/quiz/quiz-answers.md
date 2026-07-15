# Quiz Answers: Build, Configure, Deploy, and Choose an SSR Boundary

1. **What is the central rule of this module?**

   Build and type-check the production application, validate environment configuration, expose only public client values, test the deployed artifact, and choose SSR only when its server and hydration costs solve a real need.

2. **What common mistake should be avoided?**

   Do not add SSR by default, ship secrets in client variables, or deploy without checking direct URLs and rollback.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.