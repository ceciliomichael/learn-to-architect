# Module 15: Revert Published Commits

## What you will learn

You will undo the effect of a shared commit by creating a new commit instead of replacing history.

## Preserve history that other people may have

Once a commit has been pushed to a shared branch, other clones may depend on its hash and descendants. Moving the shared branch backward can force everyone to repair diverging history.

`git revert` keeps the existing commits and creates a new commit whose patch reverses a selected commit.

```text
A <- B <- C <- R  main
```

If `C` introduced the unwanted change, `R` reverses its effect. Both remain visible and the reason can be documented.

## Inspect before reverting

```text
git status
git show COMMIT
git log --graph --oneline --decorate
```

Confirm the branch, a clean working tree, and the exact commit. Then run:

```text
git revert COMMIT
```

Git prepares the inverse change and opens a commit message. Keep the generated subject unless the project needs more context.

## Revert may conflict

Later commits may have changed the same lines. If Git cannot apply the inverse cleanly:

1. Read status and the conflicted files.
2. Edit them to the final state that correctly removes the selected change while preserving later work.
3. Stage the resolved paths.
4. Continue:

```text
git revert --continue
```

Or abandon the in-progress revert:

```text
git revert --abort
```

## Reverting a merge is a team decision

A merge has multiple parents, so Git needs to know which parent represents the mainline to keep:

```text
git revert -m 1 MERGE_COMMIT
```

Do not copy `-m 1` blindly. Parent order and later re-merges affect the result. Inspect `git show --no-patch --pretty=raw MERGE_COMMIT` and coordinate with the team.

## Revert the revert

If a reverted change becomes desirable later, reverting the revert creates another normal commit. This preserves the full decision history.

## Revert compared with restore and reset

- Restore copies file content into the index or working tree.
- Revert adds a commit that reverses another commit's patch.
- Reset moves a branch and is taught next for private local history.

## Common mistakes

### Reverting the wrong hash

Read `git show COMMIT` before acting.

### Expecting the original commit to disappear

Revert preserves it and adds a new commit.

### Reverting a merge without understanding mainline

Pause and inspect both parents. Coordinate before altering a shared branch.

## Check your understanding

You are ready when you can explain why revert is suitable for shared history and verify both the original and inverse commits.
