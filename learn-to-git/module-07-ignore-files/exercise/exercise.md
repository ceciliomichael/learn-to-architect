# Exercises: Ignore Generated and Private Files

## Exercise 1: Write and test rules

1. Create `.gitignore` with rules for `build/`, `*.log`, and `.env`.
2. Create `debug.log` and `.env`.
3. Create a `build` folder containing `result.txt`.
4. Run normal status and ignored short status.
5. Ask Git which rule ignores each path.

## Exercise 2: Keep one exception

1. Add rules that ignore `*.cache` but keep `important.cache`.
2. Create `temporary.cache` and `important.cache`.
3. Confirm only the important file appears as untracked.

## Exercise 3: Share the rules

1. Stage `.gitignore` and `important.cache`.
2. Inspect the staged diff.
3. Commit them with a message explaining the ignore policy.
