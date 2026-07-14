# Quiz Answers: Pinia and Shared Application State

1. **What is the central rule of this module?**

   Pinia stores shared application state and actions when ownership truly spans distant components. Keep local component state local and expose focused store APIs.

2. **What common mistake should be avoided?**

   Do not create one store for every value or let components mutate unrelated store details freely.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.