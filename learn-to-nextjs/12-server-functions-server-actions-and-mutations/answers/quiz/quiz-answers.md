# Quiz Answers: Server Functions, Server Actions, and Mutations

1. **What is the central rule of this module?**

   A server function runs trusted server code, and a server action can be invoked as a mutation endpoint from the UI. Validate input and authenticate and authorize every call.

2. **What common mistake should be avoided?**

   Do not trust an action merely because its calling button was rendered by your application.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.