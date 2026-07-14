# Quiz Answers: Vue Playground, create-vue, and the Application Root

1. **What is the central rule of this module?**

   Use the official playground for a quick experiment or create-vue for a local strict TypeScript project, then identify the application root and the component mounted into it.

2. **What common mistake should be avoided?**

   Do not add Vue through unrelated scripts or hide the mount element and entry file before understanding their roles.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.