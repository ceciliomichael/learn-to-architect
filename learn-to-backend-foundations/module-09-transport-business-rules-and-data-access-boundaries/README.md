# Module 09: Transport, Business Rules, and Data Access Boundaries

## What you will learn

This module focuses on **Transport, Business Rules, and Data Access Boundaries** as part of Backend Foundations. The goal is to understand the responsibility, use it in a language-neutral HTTP service design that can be implemented in any backend track, and collect evidence that the result remains correct when input, dependencies, or timing change.

## Start with the plain idea

Do not begin by memorizing a command or framework option. First identify the problem this topic solves, the information it receives, the decisions it owns, the side effects it may cause, and the result another part of the system expects.

For this module, write down five things before implementation:

1. The input and where it came from.
2. The assumptions that must be checked at runtime.
3. The rule or transformation the module owns.
4. The external work, stored state, or user-visible effect it can change.
5. The evidence that proves success, failure, and recovery behave correctly.

## Topic guide

- Transport code translates HTTP into application input, business code enforces policy, and data access code owns persistence details.
- Dependencies should point toward stable rules rather than making rules depend on a framework request object.
- Follow one request through validation, authorization, transaction, response, and telemetry.

## A reliable working model

- **Contract:** Describe accepted input and produced output in language a teammate can review.
- **Boundary:** Treat files, requests, databases, queues, model output, environment values, and third-party results as untrusted until checked.
- **Ownership:** Give timeouts, retries, cleanup, cancellation, transactions, and rollback to the code that starts the work.
- **Failure:** Decide how errors are reported, which work can be retried, and how partial changes are prevented or repaired.
- **Evidence:** Use tests, logs, metrics, traces, query plans, or inspected output that match the risk of the change.

## Worked scenario

```text
Topic: Transport, Business Rules, and Data Access Boundaries
Project: a language-neutral HTTP service design that can be implemented in any backend track

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

Continue to [Module 10](../module-10-startup-readiness-graceful-shutdown-and-cancellation/README.md).