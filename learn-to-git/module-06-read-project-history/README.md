# Module 06: Read Project History

## What you will learn

You will read commit history, inspect one commit, follow a file, and use commit identifiers.

## Read the log

Start with:

```text
git log
```

The newest commit appears first. Each entry includes a full hash, author, date, and message. Press `q` if Git opens a pager and you want to return to the prompt.

A compact view is useful for orientation:

```text
git log --oneline --decorate
```

`--decorate` shows names such as branches and tags beside the commits they identify.

## Understand commit names

A commit hash uniquely identifies content and history in the repository. Commands often accept an unambiguous short prefix.

Git also supports relative names:

- `HEAD` is the checked-out commit.
- `HEAD^` is its first parent.
- `HEAD~2` follows first-parent links two times.

These names do not create copies. They identify existing commits.

## Inspect one commit

Run:

```text
git show HEAD
```

This displays commit information and its patch. Useful variations are:

```text
git show --stat HEAD
git show --name-only --format=fuller HEAD
```

Replace `HEAD` with a branch, tag, or hash to inspect another commit.

## See how history branches

This view becomes especially useful after later branching modules:

```text
git log --graph --oneline --decorate --all
```

`--all` asks the log to start from all references, not only the current branch.

## Follow one file

Show commits that affect a path:

```text
git log -- notes.txt
```

To follow a file across detected renames:

```text
git log --follow -- first.txt
```

`--follow` is intended for a single path and uses rename detection. It is a history view, not permanent rename metadata.

## Search commit messages

```text
git log --oneline --grep="diff"
```

This searches commit messages. Later investigation tools will search content and identify bug-introducing commits.

## Common mistakes

### Treating the short hash as a fixed length

A short hash only needs to be unambiguous in the repository. Copy what Git prints instead of assuming a length.

### Assuming log changes history

Log and show are inspection commands. They do not move branches or edit commits.

### Looking only at commit messages

Use `git show` when you need evidence of the actual patch.

## Check your understanding

You are ready when you can find a commit, identify its parent, inspect its patch, and limit history to one file.
