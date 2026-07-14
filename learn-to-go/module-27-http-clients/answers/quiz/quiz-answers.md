# Quiz Answers: HTTP Clients

1. It reuses transports and connections and centralizes timeout and redirect policy.
2. No. A response with status 500 is still a completed HTTP exchange and must be checked.
3. It releases resources and permits connection reuse after the body is handled.
4. To bound memory and work from an untrusted peer.
5. It may reach internal, local, or metadata services that the external user cannot access directly.
