# Exercises: HTTP Clients

1. Use `httptest.Server` as a local JSON service.
2. Call it with a reusable client and request context.
3. Reject non-200 status before decoding.
4. Limit the body to 4 KiB and validate decoded fields.
5. Add a short timeout and prove a slow handler is cancelled.
