# Quiz Answers: Errors, Defer, Panic, and Recovery Boundaries

1. The operation succeeded with no reported failure.
2. `%w` in `fmt.Errorf`.
3. Wrapped context can change displayed text while the underlying error identity remains inspectable.
4. When the surrounding function returns, in reverse order of registration.
5. No. Returned errors describe expected failures and should be handled or propagated explicitly.
