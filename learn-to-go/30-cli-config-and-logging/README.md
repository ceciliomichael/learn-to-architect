# Module 30: Command-Line Programs, Configuration, and Logging

## What you will learn

You will parse command arguments, validate environment configuration, return useful exit codes, and write secret-safe structured logs.

Use a dedicated `flag.FlagSet` so parsing can be tested without process-global state. Parsing belongs at the command edge; pass ordinary validated values to domain functions.

Environment variables are untrusted strings. Validate presence, type, range, allowed values, and path policy once at startup. Environment variables are not automatically secret and can appear in diagnostics or child processes.

`log/slog` records structured operational events. Log stable event names and useful non-sensitive fields. Never log passwords, tokens, authorization headers, connection strings, raw personal records, or entire untrusted bodies.

Normal command results go to stdout. Help and diagnostics go to stderr. Return an exit code from a `run` function, then call `os.Exit` only from `main`, after work that needs deferred cleanup has returned.

```go
func main() {
	os.Exit(run(os.Args[1:], os.Stdout, os.Stderr))
}
```

Document exit codes for automation. Commonly, zero means success, two means usage or validation failure, and one means an operational failure, but the contract belongs to the command.

## Check your understanding

You are ready when you can separate parsing, validation, domain work, user output, logs, and process exit.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
