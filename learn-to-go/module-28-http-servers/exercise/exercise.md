# Exercises: HTTP Servers and Middleware

1. Build a GET health handler with JSON content type.
2. Return 405 for another method and include the `Allow` header.
3. Add middleware that sets a fixed practice request ID.
4. Test status, headers, and body with `httptest`.
5. Configure a server with explicit timeouts and outline graceful shutdown.
