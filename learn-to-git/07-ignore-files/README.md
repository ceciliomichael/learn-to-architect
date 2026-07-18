# Module 07: Ignore Generated and Private Files

## What you will learn

You will write `.gitignore` rules, test them, and understand why ignore rules do not affect files already tracked.

## What should stay out of commits

Projects often produce files that should not become shared history:

- Generated build output
- Dependency folders that can be recreated
- Editor or operating system clutter
- Local configuration
- Files containing secrets

Ignoring a secret does not make it safe if it was already committed. Never commit passwords, tokens, or private keys.

## Create `.gitignore`

Create a plain text file named `.gitignore` at the repository root:

```text
build/
*.log
.env
```

The rules mean:

- `build/` ignores directories named `build` and their contents.
- `*.log` ignores names ending in `.log`.
- `.env` ignores that name at any level unless the pattern is anchored.

Commit `.gitignore` so everyone receives the shared rules.

## Useful pattern rules

```text
/output/
notes/*.tmp
*.cache
!keep.cache
```

- A leading `/` anchors the pattern to the `.gitignore` file's folder.
- `*` matches characters within one path level.
- `**` can match across path levels.
- A leading `!` negates an earlier match.

Re-including a file inside an excluded directory can require rules that also re-include its parent directories. Prefer clear, narrow patterns.

## Test a rule

Ask which rule ignores a path:

```text
git check-ignore -v debug.log
```

The output names the ignore file, line, pattern, and path. No output means no ignore rule matched.

To show ignored files in status:

```text
git status --ignored --short
```

## Tracked files are not affected

If Git already tracks `.env`, adding it to `.gitignore` does not remove it from history or stop tracking it.

To remove it from the next snapshot while keeping the working file:

```text
git rm --cached .env
git commit -m "Stop tracking local environment file"
```

This does not erase the file from older commits. If the file contained a real secret, revoke or rotate the secret immediately. History cleanup is a separate coordinated task.

## Common mistakes

### Treating `.gitignore` as security

It only affects untracked path selection. It does not encrypt, delete, or protect content.

### Ignoring too broadly

A pattern such as `*.json` may hide important project files. Ignore only reproducible or local content.

### Forgetting to commit `.gitignore`

Shared rules help the whole team avoid accidental additions.

## Check your understanding

You are ready when you can explain a pattern, test it, and state what to do when the file is already tracked.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
