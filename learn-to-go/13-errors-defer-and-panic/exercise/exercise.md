# Exercises: Errors, Defer, Panic, and Recovery Boundaries

1. Validate a positive quantity with a sentinel error.
2. Wrap the error with operation context and prove `errors.Is` still finds it.
3. Wrap an insufficient-stock sentinel with requested and available counts.
4. Use defer to print cleanup after a function's main work.
5. Explain why invalid user input should not cause panic.
