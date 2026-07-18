# Module 27: HTTP Clients

## What you will learn

You will make bounded HTTP requests, reuse a configured client, validate status and content, and always close response bodies.

```go
request, err := http.NewRequestWithContext(ctx, http.MethodGet, endpoint, nil)
if err != nil {
	return err
}
response, err := client.Do(request)
if err != nil {
	return err
}
defer response.Body.Close()
```

Create one reusable `http.Client` with a total timeout appropriate to the operation. Creating clients per request loses connection reuse. The default client has no overall timeout, which is unsafe for many commands and services.

HTTP status outside the expected range is not automatically a Go error. Check it before decoding. Limit the response body with `io.LimitReader`, validate content type when the contract requires it, decode one expected shape, and validate its fields.

Build URLs with `net/url`, not string concatenation. Restrict schemes and destinations when external input influences a request to reduce server-side request forgery risk. Redirects can change the destination and may need a policy.

Transport errors, timeout errors, status failures, and invalid bodies mean different things. Preserve useful causes without exposing tokens, URLs containing secrets, or private response bodies.

## Check your understanding

You are ready when every request has a context, timeout, destination policy, body limit, close, status check, and validation step.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
