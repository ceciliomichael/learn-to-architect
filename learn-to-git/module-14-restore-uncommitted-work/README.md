# Module 14: Restore Uncommitted Work

## What you will learn

You will correct the staging area, restore tracked working files, and preview removal of untracked files.

## First identify where the unwanted change lives

Run all three inspections:

```text
git status
git diff
git diff --staged
```

Ask:

- Is the change only in the working tree?
- Is it staged?
- Is the path untracked?
- Is there already a commit to undo?

This module is only for uncommitted work. Later modules handle commits.

## Unstage without discarding the working edit

```text
git restore --staged notes.txt
```

This restores the index version from `HEAD` by default. The working tree content remains edited.

Inspect again before doing anything else.

## Discard an unstaged tracked edit

```text
git restore notes.txt
```

By default, this copies the index version into the working tree. The discarded working content is normally not recoverable through Git because it was never stored as an object you deliberately kept.

Before running it:

1. Read `git diff -- notes.txt`.
2. Copy the content elsewhere if any part may matter.
3. Confirm the exact path.

## Restore from a chosen commit

Copy one path from an earlier commit into the working tree:

```text
git restore --source=HEAD^ -- notes.txt
```

This does not move `HEAD` or the branch. It creates a working tree change that you can inspect, stage, and commit if desired.

Restore both the index and working tree from `HEAD`:

```text
git restore --source=HEAD --staged --worktree -- notes.txt
```

That command discards staged and unstaged changes to the path. Use it only after careful inspection.

## Untracked files are different

`git restore` does not normally delete an untracked file because the index has no tracked version for it.

Preview which untracked files Git could remove:

```text
git clean -n
```

`-n` is a dry run and removes nothing. To include untracked directories in the preview:

```text
git clean -nd
```

Actual `git clean -f` removal is permanent from Git's point of view. Prefer normal file tools for one known disposable path, or make a backup before cleaning.

## A practical decision guide

- Wrong file staged, edit should stay: `git restore --staged path`
- Wrong unstaged edit to a tracked file: inspect, then `git restore path`
- Need an old file as a new edit: `git restore --source=COMMIT -- path`
- Untracked file: inspect it and use normal file tools, or preview `git clean -n`

## Common mistakes

### Thinking a backup branch saves uncommitted text

A branch points to a commit. It does not capture uncommitted content. Copy, commit, or stash that content first.

### Omitting `--staged` when only the index is wrong

Plain restore changes the working tree. State the target location explicitly.

### Running clean without a preview

Always use `-n` and inspect every candidate path first.

## Check your understanding

You are ready when you can identify the location of an uncommitted change and choose a command that affects only the intended location.
