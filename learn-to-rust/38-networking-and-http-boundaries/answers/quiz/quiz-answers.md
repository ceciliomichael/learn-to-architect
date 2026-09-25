# Quiz Answers: Module 38

## 1

An HTTP 500 means a protocol response was received from a server, while a connection failure may mean no HTTP exchange was established. Recovery and diagnostics differ.

## 2

The server may already have applied a non-idempotent change before the client lost or timed out waiting for the response, so repeating it can duplicate effects.

## 3

It can reuse connection pools and centralize configuration such as timeouts, proxies, and TLS behavior.

## 4

It removes authentication of the remote endpoint and exposes traffic to interception rather than solving the underlying certificate or trust configuration problem.

## 5

A remote peer can send very large or slow content, consuming memory, bandwidth, CPU, and time unless your application enforces limits.
