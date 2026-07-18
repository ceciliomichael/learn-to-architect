# Module 23: Work in Two Branches with Worktrees

## What you will learn

You will attach additional working trees to one repository, work on separate branches, and remove a worktree safely.

## Why use a worktree

A normal repository has one main working tree. Switching changes which branch its files show. Sometimes you need to keep a long-running edit open while checking another branch immediately.

`git worktree` can create another working directory connected to the same repository data. Each worktree has its own checked-out branch, working files, and index.

This is lighter than making another full clone for local parallel work, but all linked worktrees share references and object storage.

## Create a worktree with a new branch

From the main working tree:

```text
git worktree add -b urgent-fix ../project-urgent-fix main
```

This creates `urgent-fix` from `main`, creates the sibling directory, and checks out the new branch there.

Attach an existing branch instead:

```text
git worktree add ../project-review review-branch
```

A branch normally cannot be checked out in two worktrees at once. This prevents two working directories from trying to update the same branch reference independently.

## Inspect linked worktrees

```text
git worktree list
```

The output shows each path, checked-out commit, and branch. In each directory, `git status` concerns that worktree's files and index.

Commits are shared immediately through the repository. If the urgent worktree creates a commit, the main worktree can see its branch and objects without fetch. The main working files do not change until you merge or switch there.

## Remove a finished worktree

First commit, discard, or move valuable changes. Then leave the directory and run from another worktree:

```text
git worktree remove ../project-urgent-fix
```

Git normally refuses if the worktree contains changes. Do not force removal until you have inspected them.

Removing a worktree does not automatically delete its branch:

```text
git branch -d urgent-fix
```

Only delete after the work is integrated or otherwise preserved.

## Prune stale records

If a linked directory was removed outside Git, preview stale administrative records:

```text
git worktree prune --dry-run --verbose
```

Then prune only after reviewing the output:

```text
git worktree prune --verbose
```

## Common mistakes

### Confusing directories during commits

Check `pwd`, `git branch --show-current`, and status in every terminal.

### Removing the folder manually

Use `git worktree remove` so Git cleans its administrative records.

### Expecting separate repository history

Linked worktrees share objects and branch references. Use separate clones when you need independent repository configuration or remote-tracking state.

## Check your understanding

You are ready when you can create a new linked worktree, state what is shared, and remove it without losing changes.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
