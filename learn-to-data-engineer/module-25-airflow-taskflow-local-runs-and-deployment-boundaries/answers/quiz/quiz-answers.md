# Quiz Answers: Airflow TaskFlow, Local Runs, and Deployment Boundaries

1. **What responsibility does this module add to the continuing project?**

   It adds Airflow TaskFlow, Local Runs, and Deployment Boundaries with an explicit input contract, owned rule, controlled side effects, failure behavior, and verification evidence.

2. **Which values must still be checked at runtime?**

   Values from requests, files, databases, queues, environment configuration, model output, users, and external services remain untrusted regardless of source-code types.

3. **Who should own retries, cancellation, cleanup, or rollback?**

   The boundary that starts and observes the external work should own its timeout, cancellation, retry policy, cleanup, and recovery decision.

4. **Why is a successful happy path insufficient evidence?**

   It does not show what happens with invalid input, repeated work, partial failure, unavailable dependencies, concurrency, interruption, or restart.

5. **What must remain out of source code and diagnostic output?**

   Passwords, tokens, private keys, connection secrets, unnecessary personal data, and full sensitive payloads must not be committed or logged.