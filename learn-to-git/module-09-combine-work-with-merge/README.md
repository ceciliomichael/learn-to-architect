# Module 09: Combine Work with Merge

## What you will learn

You will merge a branch, recognize fast-forward and three-way merges, and inspect the result.

## The branch you are on receives the merge

To bring `story-middle` into `main`:

```text
git switch main
git merge story-middle
```

Read that as: switch to the destination, then merge the named source into it. The command does not mean the named branch receives `main`.

Before merging, make the working tree clean and inspect the graph:

```text
git status
git log --graph --oneline --decorate --all
```

## Fast-forward merge

If `main` is an ancestor of `story-middle`, Git can move the `main` name forward:

```text
A <- B  main
     \
      C  story-middle
```

After a fast-forward, both names point to `C`. No merge commit is required because the history is already one direct line.

## Three-way merge

If both branches gained commits after they separated, neither tip is an ancestor of the other:

```text
      C  main
     /
A <- B
     \
      D  topic
```

Git compares the two tips and their best common ancestor. If it can combine the snapshots, it creates a merge commit with both tips as parents:

```text
      C <- M  main
     /   /
A <- B  /
     \ /
      D  topic
```

The topic branch stays at `D` until you move or delete its name.

## Force a merge commit only when policy needs one

`git merge --no-ff topic` creates a merge commit even when fast-forward is possible. Some teams use this to keep branch boundaries visible. It is not automatically better. Follow the project's history policy.

## Inspect the result

```text
git status
git log --graph --oneline --decorate --all
git show --stat HEAD
```

For a merge commit, `git show` may use a combined view. The graph is the clearest first check for its two-parent relationship.

## Delete the merged branch name

After verifying that `main` contains the work:

```text
git branch -d story-middle
```

Deleting a merged branch name does not delete the commits reachable from `main`.

## Common mistakes

### Merging while on the source branch

Always say the destination out loud, switch to it, and confirm the current branch.

### Expecting every merge to create a commit

A fast-forward moves a branch name without a new commit.

### Deleting before checking

Inspect the graph and final files first. Use `-d`, not `-D`, for normal cleanup.

## Check your understanding

You are ready when you can choose the destination branch and explain why a merge did or did not create a new commit.
