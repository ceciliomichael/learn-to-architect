# Module 14: Sessions, Cookies, CSRF, and Browser Clients

## What you will learn

This module focuses on **Sessions, Cookies, CSRF, and Browser Clients** as part of Java and Spring Backend Development. The goal is to understand the responsibility, use it in a production-oriented Java service using Spring Boot and Spring MVC, and collect evidence that the result remains correct when input, dependencies, or timing change.

## Start with the plain idea

Do not begin by memorizing a command or framework option. First identify the problem this topic solves, the information it receives, the decisions it owns, the side effects it may cause, and the result another part of the system expects.

For this module, write down five things before implementation:

1. The input and where it came from.
2. The assumptions that must be checked at runtime.
3. The rule or transformation the module owns.
4. The external work, stored state, or user-visible effect it can change.
5. The evidence that proves success, failure, and recovery behave correctly.

## Topic guide

- Authentication establishes an identity; authorization decides whether that identity may perform this action on this resource.
- Validate token issuer, audience, signature, expiry, and required claims using maintained libraries.
- Enforce ownership and tenant scope beside every protected read and write.

## A reliable working model

- **Contract:** Describe accepted input and produced output in language a teammate can review.
- **Boundary:** Treat files, requests, databases, queues, model output, environment values, and third-party results as untrusted until checked.
- **Ownership:** Give timeouts, retries, cleanup, cancellation, transactions, and rollback to the code that starts the work.
- **Failure:** Decide how errors are reported, which work can be retried, and how partial changes are prevented or repaired.
- **Evidence:** Use tests, logs, metrics, traces, query plans, or inspected output that match the risk of the change.

## Worked scenario

```text
Topic: Sessions, Cookies, CSRF, and Browser Clients
Project: a production-oriented Java service using Spring Boot and Spring MVC

Input boundary -> validation -> owned rule -> controlled side effect -> verified result
       |               |             |                 |                 |
   reject bad data   clear error   deterministic     recoverable       test and inspect
```

Walk through the scenario from left to right. A successful happy path is not enough. Also trace an invalid input, an unavailable dependency, a timeout, repeated work, and a restart where those cases apply.

## Common mistakes

- Adding a tool before explaining the responsibility it is supposed to own.
- Trusting a type annotation, generated schema, model response, or framework object without runtime evidence.
- Combining transport, business rules, storage, and operational policy in one large function.
- Retrying an operation without deciding whether repeating it is safe.
- Logging secrets, tokens, personal data, or full untrusted payloads.
- Declaring success because the example ran once instead of testing failure and recovery.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before reading the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 15](../module-15-spring-security-authentication-and-password-storage/README.md).