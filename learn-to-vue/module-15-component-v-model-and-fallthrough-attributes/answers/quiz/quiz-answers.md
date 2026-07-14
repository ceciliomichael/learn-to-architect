# Quiz Answers: Component v-model and Fallthrough Attributes

1. **What is the central rule of this module?**

   Component v-model is a prop and update event contract, while fallthrough attributes let a wrapper preserve useful HTML attributes and listeners on the intended root element.

2. **What common mistake should be avoided?**

   Do not swallow labels, accessibility attributes, classes, or listeners in a wrapper component.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.