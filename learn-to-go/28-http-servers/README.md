# Module 28: HTTP Servers and Middleware

## What you will learn

You will build small handlers, enforce request limits, test them without a network port, and shut a server down deliberately.

```go
func health(writer http.ResponseWriter, request *http.Request) {
	if request.Method != http.MethodGet {
		http.Error(writer, "method not allowed", http.StatusMethodNotAllowed)
		return
	}
	writer.Header().Set("Content-Type", "application/json")
	writer.WriteHeader(http.StatusOK)
	fmt.Fprint(writer, `{"status":"ok"}`)
}
```

Handlers validate method, path values, headers, body size, content type, authentication, authorization, and decoded fields at the edge. Authentication identifies a caller; authorization decides whether that caller may perform this action. Both belong on the server.

Middleware wraps shared boundary behavior such as request IDs, recovery, security headers, logging, and authorization. Keep the chain explicit. Recovery should return a generic response and log safe operational context, not panic details to the client.

Configure `http.Server` read-header, read, write, and idle timeouts from real workload needs. Limit bodies with `http.MaxBytesReader`. Use `httptest` for handler contracts.

On shutdown, stop accepting new work and call `Shutdown` with a deadline so active handlers have bounded time to finish.

## Check your understanding

You are ready when a request crosses validation, authorization, domain work, response encoding, and bounded shutdown without hidden global state.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
