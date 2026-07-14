# Module 27: Automate Local Checks with Hooks

## What you will learn

You will understand Git hooks, build one small local check, and know why hooks do not replace server enforcement.

## What a hook is

A hook is a program that Git runs at a documented point in an operation. Client-side hooks can run before or after commits, merges, rebases, and other local actions. Server-side hooks can evaluate pushes on a repository server.

Common client-side examples are:

- `pre-commit`: runs before Git creates a commit
- `commit-msg`: receives the commit message file path and can reject the message
- `post-commit`: runs after a commit succeeds and cannot stop that completed commit

Git checks a repository's configured hooks directory. The default is `$GIT_DIR/hooks`. Sample files often end in `.sample` and are not active.

## Hooks are programs, not Git configuration text

A hook needs a supported interpreter, appropriate permissions, and the exact expected file name without `.sample`. On Unix-like systems it must be executable. Git for Windows can run shell hooks through its included shell when written correctly.

A `commit-msg` shell hook that rejects `WIP` in a message can be:

```text
#!/bin/sh
message_file="$1"
if grep -q "WIP" "$message_file"
then
  echo "Commit message must not contain WIP."
  exit 1
fi
exit 0
```

Exit status 0 allows the operation. A nonzero result rejects it.

## Use a tracked hooks folder for a project

Files under `.git/hooks` are not committed or cloned. A team can keep hook programs in a tracked folder and configure each clone locally:

```text
git config core.hooksPath .githooks
```

The project setup guide should explain interpreter and permission requirements. The configuration itself is local unless a setup process applies it.

## Hooks can be bypassed or missing

Several commands support `--no-verify`, and a contributor may not install local hooks at all. Therefore:

- Local hooks provide fast feedback.
- Continuous integration and protected server rules enforce required checks.
- Security and authorization must never depend only on client-side hooks.

## Keep hooks small and predictable

A useful hook should:

- Finish quickly
- Print a clear reason and repair instruction on failure
- Avoid changing unrelated files unexpectedly
- Use tools documented as project requirements
- Return accurate exit statuses

Long test suites can run in continuous integration or an explicit command rather than making every local commit slow.

## Debug a hook

Check:

```text
git config --get core.hooksPath
git rev-parse --git-path hooks
```

Then verify the file name, interpreter line, executable permission where required, dependencies, and exit status. Run the hook program directly with safe test input when possible.

## Common mistakes

### Expecting `.git/hooks` to clone

It lives in local Git administration and is not tracked project content.

### Making rejection mysterious

Print the exact rule and how the contributor can correct it.

### Treating a local hook as access control

Enforce protected actions on the server.

## Check your understanding

You are ready when you can explain when a hook runs, what its exit status means, and where required policy must be enforced.
