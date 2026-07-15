# Quiz Answers: Unit and Component Testing

1. **What is the central rule of this module?**

   Unit tests cover isolated rules and component tests cover rendered behavior at the smallest useful boundary. Mock only the external boundary the test does not own.

2. **What common mistake should be avoided?**

   Do not test framework internals or replace all server behavior with mocks that can never detect integration mistakes.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.