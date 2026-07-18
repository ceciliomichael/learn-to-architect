# Module 12: Fetch and Remote-Tracking Branches

## What you will learn

You will fetch remote data, inspect remote-tracking branches, and measure whether histories are ahead or behind.

## Fetch updates your knowledge

Run inside a clone:

```text
git fetch origin
```

Fetch contacts `origin`, downloads needed Git objects and references, and updates local remote-tracking names such as `origin/main`. It does not normally merge those commits into your current local branch or rewrite your working files.

This separation makes fetch a useful inspection step.

## Remote-tracking branches are local records

`origin/main` is not the branch stored inside the remote repository. It is your repository's local record of where `origin` reported its `main` branch during the latest successful communication.

The names can differ:

```text
main         your local branch
origin/main  your local record of origin's main
```

If another person changes the remote, your `origin/main` remains old until you fetch again.

List remote-tracking names:

```text
git branch --remotes
```

See local and remote-tracking names together:

```text
git branch --all
git log --graph --oneline --decorate --all
```

## Compare ahead and behind work

Commits reachable from `origin/main` but not `main`:

```text
git log --oneline main..origin/main
```

Commits reachable from `main` but not `origin/main`:

```text
git log --oneline origin/main..main
```

Count both directions:

```text
git rev-list --left-right --count main...origin/main
```

The first number is unique to the left name, and the second is unique to the right name.

## Upstream tracking configuration

A local branch can have an upstream branch used as its default comparison and exchange target. Inspect it with:

```text
git branch -vv
```

A local `main` created by clone normally tracks `origin/main`. Tracking does not mean continuous synchronization. It supplies defaults and ahead or behind information based on your last fetch.

Set an upstream explicitly when needed:

```text
git branch --set-upstream-to=origin/main main
```

## Remove stale remote-tracking names

If a branch was deleted on the remote, prune its old local record while fetching:

```text
git fetch --prune origin
```

This removes stale remote-tracking references. It does not delete your local branches.

## Common mistakes

### Expecting fetch to update the working file

Fetch updates remote-tracking information. A later merge or rebase integrates it into a local branch.

### Treating `origin/main` as live network state

It only reflects the most recent fetch or push that updated it.

### Reading ahead and behind without fetching

Fetch first when current remote state matters.

## Check your understanding

You are ready when you can fetch, explain `origin/main`, and show the commits unique to either side.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
