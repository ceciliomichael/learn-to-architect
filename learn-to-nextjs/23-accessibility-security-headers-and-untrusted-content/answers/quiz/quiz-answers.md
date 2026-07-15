# Quiz Answers: Accessibility, Security Headers, and Untrusted Content

1. **What is the central rule of this module?**

   Preserve semantic HTML and keyboard behavior, apply security headers deliberately, validate untrusted content, and avoid rendering raw HTML unless it has a proven sanitization boundary.

2. **What common mistake should be avoided?**

   Do not consider TypeScript, React escaping, or a Content Security Policy a replacement for input validation and authorization.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.