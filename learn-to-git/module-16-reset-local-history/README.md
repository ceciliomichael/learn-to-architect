# Module 16: Reset Local History

## What you will learn

You will move a private local branch with reset and predict what happens to the index and working tree.

## Reset is for history you control

Reset can move the current branch to another commit. If commits were already shared, moving the branch can conflict with other clones. Use revert for ordinary shared history.

Before reset:

```text
git status
git log --graph --oneline --decorate --all
git branch backup-before-reset
```

The backup branch gives the current commit a stable name. It protects committed work, not uncommitted edits.

## The three reset modes

Suppose `HEAD` points to `C` and you reset to parent `B`.

### Soft reset

```text
git reset --soft HEAD^
```

The branch moves to `B`. The index and working tree stay as they were at `C`. The old commit's change is therefore staged.

Use this when a private last commit should be rebuilt while keeping its exact snapshot staged.

### Mixed reset

```text
git reset --mixed HEAD^
```

`--mixed` is the default mode. The branch moves to `B`, the index is reset to `B`, and the working tree stays as it was. The old commit's change becomes unstaged.

### Hard reset

```text
git reset --hard HEAD^
```

The branch, index, and tracked working tree paths are reset to `B`. Tracked edits that differ from the target are discarded. Untracked files are generally not removed, although an untracked path can be removed if it blocks writing a tracked path.

Use hard reset only in a disposable repository or after verifying that everything valuable exists in a commit or separate backup.

## Reset does not erase objects immediately

The old commit may no longer be named by the current branch, but its object usually remains for a time and its former location is normally recorded in the local reflog. Module 17 practices recovery. This is a recovery opportunity, not a backup promise.

## A safe way to compare modes

In a disposable repository:

1. Create a backup branch at the latest commit.
2. Try one reset mode.
3. Inspect branch location, staged diff, unstaged diff, and file content.
4. Return to the backup commit before trying the next mode.

## Reset with a path is different

Commands such as `git reset HEAD -- path` reset index entries without moving the branch. This course uses the clearer `git restore --staged path` for that job.

## Common mistakes

### Using hard reset to unstage

Hard reset changes far more than the index. Use restore with `--staged`.

### Resetting a shared branch

Other contributors may have based work on the removed commit names. Revert shared mistakes.

### Assuming the backup branch saved working edits

It only names a commit. Commit, stash, or separately copy uncommitted work.

## Check your understanding

You are ready when you can predict the branch, index, and working tree state for soft, mixed, and hard reset.
