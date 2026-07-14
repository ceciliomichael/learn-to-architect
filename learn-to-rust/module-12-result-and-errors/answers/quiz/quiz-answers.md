# Quiz Answers: Recoverable Errors with Result

1. `Ok(T)` and `Err(E)`.
2. It returns early with a converted error.
3. No. Return errors so the application boundary chooses reporting.
4. Callers can distinguish expected categories without parsing text.
5. No. Return a recoverable error.
