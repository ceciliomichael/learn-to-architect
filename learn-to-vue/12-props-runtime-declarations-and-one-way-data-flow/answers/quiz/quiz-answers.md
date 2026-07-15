# Quiz Answers: Props, Runtime Declarations, and One-Way Data Flow

1. **What is the central rule of this module?**

   Props are one-way readonly inputs. Type declarations help authors, runtime declarations can validate JavaScript callers, and object or array defaults must not be shared mutable instances.

2. **What common mistake should be avoided?**

   Do not mutate a prop inside a child or copy it into state without a clear editable-draft reason.

3. **Which runtime values can remain untrusted even when TypeScript accepts the source?**

   URL values, forms, storage, network responses, cookies, environment-derived values, and third-party code remain runtime boundaries.

4. **Which user-facing states must remain accessible?**

   Normal, keyboard focus, loading, empty, invalid, error, success, and disabled states that the feature can produce.

5. **What evidence should be collected before considering the exercise complete?**

   Strict type results, automated tests, rendered DOM and accessibility inspection, browser diagnostics, and observed failure and recovery behavior.