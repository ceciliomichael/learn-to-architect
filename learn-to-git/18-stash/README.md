# Module 18: Set Work Aside with Stash

## What you will learn

You will temporarily store tracked changes, include untracked files deliberately, restore a stash, and handle conflicts.

## When stash helps

Sometimes you need a clean working tree before switching tasks, but the current change is not ready for a meaningful commit. A stash records selected working tree and index changes in repository objects and then cleans those changes from the working area.

Stash is temporary task management, not a replacement for clear commits or backups.

## Create a named stash

Inspect first:

```text
git status
git diff
git diff --staged
git stash push -m "draft welcome text"
git status
```

By default, stash includes staged and unstaged changes to tracked files. It does not include ordinary untracked files.

Include untracked files deliberately:

```text
git stash push -u -m "draft with new file"
```

`-a` also includes ignored files and is much broader. Avoid it unless you have inspected exactly what will be stored.

## Inspect stored entries

```text
git stash list
git stash show --stat stash@{0}
git stash show -p stash@{0}
```

`stash@{0}` is normally the newest entry. In PowerShell, quote this selector if the shell interprets braces unexpectedly:

```text
git stash show -p "stash@{0}"
```

## Apply or pop

Apply the changes while keeping the stash entry:

```text
git stash apply stash@{0}
```

Apply and then drop the entry if application succeeds:

```text
git stash pop
```

Prefer `apply` when the work is important because you can inspect and test before dropping it:

```text
git stash drop stash@{0}
```

## Conflicts during application

If the current branch changed the same lines, apply or pop may conflict. Use the conflict skills from Module 10: inspect status, edit the intended result, stage resolved paths, and test.

A conflicted pop normally keeps the stash entry because it could not complete cleanly. Confirm with `git stash list` before dropping anything.

## Recover on a branch

When the original base matters, this command creates a new branch at the commit where the stash was made, applies the stash, and drops it if successful:

```text
git stash branch resume-draft stash@{0}
```

This often avoids conflicts caused by applying old work to a much newer branch.

## Common mistakes

### Assuming untracked files were included

Use `-u` and verify status after stashing.

### Popping without inspecting the entry

Read `stash show -p` and confirm the target branch first.

### Keeping important work only in a stash for months

Turn valuable work into a clear branch and commits, then back it up appropriately.

## Check your understanding

You are ready when you can create a named stash, prove what it contains, restore it safely, and explain the difference between apply and pop.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
