# Quiz Answers: Metadata, Social Images, and Document Information

1. **What is the central rule of this module?**

   Metadata describes pages to browsers and sharing services. Use a static metadata export for fixed values and generateMetadata for values that depend on route data.

2. **What common mistake should be avoided?**

   Do not update the document title from a client effect when the server can produce correct metadata before the page arrives.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.