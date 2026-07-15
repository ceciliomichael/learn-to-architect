# Module 19: Rebase a Private Branch

## What you will learn

You will replay private branch work on a newer base, resolve a rebase conflict, and recognize when not to rebase.

## What rebase changes

Suppose `topic` and `main` diverged:

```text
      C <- D  main
     /
A <- B
     \
      E <- F  topic
```

While on `topic`, run:

```text
git rebase main
```

Git finds the commits unique to `topic`, resets the branch base to `main`, and replays their changes one by one:

```text
A <- B <- C <- D  main
               \
                E' <- F'  topic
```

`E'` and `F'` are new commits with new parent relationships and therefore new hashes. Rebase does not move the original `main` branch.

## When rebase is appropriate

Rebase is useful for a private topic branch that only you use. It can make the branch appear as if it began from the current target, which may simplify later review and fast-forward integration.

Do not rebase commits that other people may already use unless the whole team coordinates. Rewriting shared hashes makes their existing descendants disagree with yours.

## Prepare and run

```text
git status
git fetch origin
git log --graph --oneline --decorate --all
git switch topic
git branch backup-topic-before-rebase
git rebase main
```

Fetch is needed only when a remote is involved. Choose the actual target reference according to team policy. Make the worktree clean and create a temporary backup name before learning or doing a complex rewrite.

## Resolve a rebase conflict

Rebase replays commits separately, so it may stop more than once.

At each stop:

```text
git status
```

Edit the correct final content, stage each resolved path, then continue:

```text
git add path
git rebase --continue
```

Other choices are:

```text
git rebase --abort
git rebase --skip
```

Abort returns to the pre-rebase state. Skip omits the current commit and should be used only when you have proved its change is already present or unwanted.

## Publishing a rewritten personal branch

If the previous version of your personal topic branch was already pushed, a normal push may be rejected. After fetching and verifying no one else added work, teams often use:

```text
git push --force-with-lease origin topic
```

The lease refuses if the remote branch is not at the position your repository expects. It is safer than plain force, but it still rewrites remote history. Never use it on a shared branch without explicit team policy.

## Common mistakes

### Expecting hashes to remain the same

New parents mean new commit identities.

### Rebasing while on the target branch

Switch to the private branch that should be replayed, then name its new base.

### Skipping a conflict blindly

Skip drops that commit from the replay. Inspect its intended change first.

## Check your understanding

You are ready when you can draw the before and after graphs, explain the new hashes, and choose abort or continue during a conflict.
