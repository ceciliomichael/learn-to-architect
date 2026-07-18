# Module 30: Command-Line Programs, Configuration, and Logging

A useful command-line program has a predictable input contract, helpful errors, and meaningful exit status. `std::env::args_os` preserves operating-system text that may not be valid UTF-8. Use `args` only when invalid UTF-8 should be rejected.

Separate three stages:

1. Collect raw arguments and environment values.
2. Parse and validate them into a typed configuration.
3. Run domain behavior using only that validated configuration.

Write normal results to stdout and diagnostics to stderr with `eprintln!`. Return a nonzero exit code when the requested work fails. Do not print secrets, tokens, full environment dumps, or sensitive user data in errors or logs.

Environment variables and configuration files are still external input. Check missing values, ranges, allowed choices, and conflicts. Define precedence, such as command line over environment over a safe default, and document it.

Structured logging libraries can attach fields and levels to events. Keep field names stable, redact sensitive values, and avoid recording large request bodies. Logs should help explain an event without becoming a second unsafe data store.

Small parsing functions are easy to unit test because they can accept an iterator or slice instead of reading global process state directly.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 31](../31-declarative-macros/README.md).
