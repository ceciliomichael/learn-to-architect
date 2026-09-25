# Exercises: Module 38

Work locally and explain your choices.

## 1. Trace

If a POST times out after sending bytes, can the client safely assume the server did nothing?

## 2. Repair

Replace an unwrap-based HTTP request with Result propagation, explicit timeout configuration, and status validation.

## 3. Modify

Change the demonstration so it prints only status and at most a deliberately bounded amount of response data rather than always buffering an unknown full body.

## 4. Build

Create an endpoint checker for a fixed operator-provided list of HTTPS URLs. Reuse one client, bound concurrent requests, record transport/status/timeout outcomes separately, and produce a summary without treating a failed endpoint as a process panic.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
