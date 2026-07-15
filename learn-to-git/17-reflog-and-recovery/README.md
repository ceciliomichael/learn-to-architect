# Module 17: Reflog, Detached HEAD, and Recovery

## What you will learn

You will use the local reflog to find former branch positions, understand detached `HEAD`, and attach a recovered commit to a branch.

## What the reflog records

References move when you commit, switch, merge, rebase, and reset. Git normally keeps local logs of these movements.

```text
git reflog
```

A line may show a commit, a selector such as `HEAD@{2}`, and a description of the action. The newest entry is first.

Unlike `git log`, which walks commit parent links, reflog answers where a local reference was recently positioned. Reflogs are local. Another clone does not receive yours through push or fetch.

Reflog entries expire according to configuration and unreachable objects can later be pruned. Use reflog for recent recovery, not as a permanent backup.

## Recover a branch after reset

Suppose an accidental reset moved `main` away from a wanted commit:

```text
git reflog
git show RECOVERED_HASH
git branch recovered-work RECOVERED_HASH
```

Inspect the candidate with `git show` before naming it. Creating a recovery branch is safer than immediately resetting again because it preserves both current and recovered positions.

## Detached HEAD

Normally `HEAD` refers to a branch. You can instead check out a specific commit for inspection:

```text
git switch --detach COMMIT
```

Now `HEAD` points directly to a commit. No local branch is current. This is called detached `HEAD`.

It is safe for reading files, running tests, or building an older version. If you commit while detached, the new commit is valid, but no branch name automatically follows it.

## Keep a detached commit

While still on the wanted detached commit:

```text
git switch -c recovered-experiment
```

If you already switched away, find the commit in the reflog, inspect it, and create a branch at its hash.

## A calm recovery process

1. Stop changing history.
2. Run status and record the current branch.
3. Read the graph and reflog.
4. Inspect candidate commits with `git show`.
5. Create new branch names for valuable candidates.
6. Compare and test before merging or resetting anything.

Creating names is safer than making more destructive moves while uncertain.

## What reflog cannot recover reliably

Reflog does not record every unsaved or uncommitted edit. It may not help after expiration, garbage collection, repository deletion, or damage. Maintain real backups and remote copies of important committed work.

## Common mistakes

### Resetting repeatedly during panic

Each extra move makes the situation harder to reason about. Inspect first and create recovery branches.

### Assuming detached means broken

It is a normal state for inspecting a commit. The main risk is leaving new commits without a branch name.

### Treating reflog as shared backup

It is local and temporary by design.

## Check your understanding

You are ready when you can find a recent former position, verify it, and give it a branch name without moving existing branches.
