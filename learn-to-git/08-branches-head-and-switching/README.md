# Module 08: Branches, HEAD, and Switching

## What you will learn

You will understand commit graphs, branch names, `HEAD`, and safe branch switching.

## A branch is a movable name

A Git branch is a name that points to one commit. When you create a commit while that branch is current, the branch name moves to the new commit.

Suppose history is:

```text
A <- B <- C  main
```

Each arrow means the newer commit records the older commit as its parent. `main` points to `C`.

Create another branch at the same commit:

```text
git branch topic
```

Now both names point to `C`. No files or commits were copied.

## HEAD tells Git what is checked out

In normal branch work, `HEAD` refers to the current branch, and that branch refers to a commit:

```text
HEAD -> main -> C
```

Show the current branch:

```text
git branch --show-current
```

List branches:

```text
git branch
```

The `*` marks the current branch.

## Create and switch in one command

```text
git switch -c topic
```

`-c` creates `topic` at the current commit and switches to it. Now `HEAD` refers to `topic`.

After a new commit on `topic`, the graph is:

```text
          D  topic <- HEAD
         /
A <- B <- C  main
```

Only `topic` moved. `main` still points to `C`.

Switch back:

```text
git switch main
```

Git updates the working tree and index to match the selected commit. Files can appear, disappear, or change because you asked to check out another snapshot.

## Switching with uncommitted changes

Git may carry a harmless uncommitted change across a switch. If switching would overwrite that change, Git normally stops and asks you to commit, stash, or discard it first.

Do not use a force or discard option merely to make the warning disappear. Run status and diff, then decide what the work means.

## Name branches clearly

Names such as `fix-total` or `add-help-page` explain the purpose. Git permits slashes, so teams often use names such as `fix/total`.

Rename the current branch:

```text
git branch -m better-name
```

## Delete a merged practice branch

You cannot delete the current branch. Switch away, then use the safe deletion form:

```text
git branch -d topic
```

`-d` refuses when Git sees commits that are not merged into an appropriate upstream or current branch. `-D` forces deletion and can make work harder to find, so it is not the normal choice.

## Common mistakes

### Thinking a branch copies every file

A branch starts as a small reference to a commit.

### Creating a branch but not switching

`git branch topic` only creates the name. `git switch -c topic` creates and switches.

### Forgetting which branch receives a commit

Run `git branch --show-current` and `git status` before committing.

## Check your understanding

You are ready when you can draw two branch names on a commit graph and predict which name moves after the next commit.
