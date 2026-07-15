# Quiz Answers: App Router Folders, Files, and Colocation

1. **What is the central rule of this module?**

   Inside app, folders organize route segments while special file names such as page, layout, loading, error, and route give files framework meaning. Ordinary colocated files are not public routes by themselves.

2. **What common mistake should be avoided?**

   Do not assume every file under app becomes a page or scatter one feature across unrelated folders.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.