# Quiz Answers: CSS, Images, Fonts, and Static Assets

1. **What is the central rule of this module?**

   Use scoped or global CSS deliberately, next/image for sized and optimized images, next/font for controlled font loading, and public for files that truly need stable public URLs.

2. **What common mistake should be avoided?**

   Do not omit image dimensions, expose private files through public, or load application fonts through avoidable render-blocking requests.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.