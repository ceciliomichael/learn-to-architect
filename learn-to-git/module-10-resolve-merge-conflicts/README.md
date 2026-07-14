# Module 10: Resolve Merge Conflicts

## What you will learn

You will understand why a merge conflicts, resolve a text conflict, and safely abort when you are not ready.

## A conflict is a request for a decision

Git combines many independent changes automatically. It stops when it cannot choose a correct final result, such as when both branches change the same lines differently.

A conflict does not mean the repository is broken. The merge is paused so a person can decide the final content.

## Start from a clean state

Before merging:

```text
git status
git branch --show-current
git log --graph --oneline --decorate --all
```

Commit or deliberately set aside unrelated work before starting.

## Read the paused merge

When a conflict occurs, run:

```text
git status
git diff
```

Status names unmerged paths. A conflicted text file may contain markers like:

```text
<<<<<<< HEAD
Ending from the current branch.
=======
Ending from the branch being merged.
>>>>>>> alternate-ending
```

The top block is from `HEAD`, which is the current destination branch. The bottom block is from the named branch. The final file can use the top, bottom, both, or a new result. The correct choice depends on the project, not on Git.

## Resolve carefully

1. Open every unmerged file.
2. Decide the correct final content.
3. Delete all marker lines.
4. Save and test the result when the project has tests.
5. Stage each resolved path.
6. Confirm status shows no unmerged paths.
7. Finish the merge commit.

Commands may look like:

```text
git add story.txt
git status
git diff --staged
git commit
```

`git commit` opens the prepared merge message in your editor. You may accept it or add useful context.

## Abort the merge

If you are not ready to resolve it:

```text
git merge --abort
```

This tries to return to the state before the merge. It is most reliable when the merge began with a clean working tree. Inspect status afterward.

## Other conflict types

A file may be deleted on one branch and modified on another. Two branches may rename paths differently. Binary files usually cannot be combined line by line. In every case, status names the unresolved paths and a person chooses the desired final snapshot.

## Common mistakes

### Committing marker lines

Search the resolved file for `<<<<<<<`, `=======`, and `>>>>>>>` before staging.

### Running merge again during the conflict

The merge is already in progress. Resolve and commit it, or abort it.

### Choosing a side without understanding the behavior

Read both changes and test the combined result. A syntactically clean file can still behave incorrectly.

## Check your understanding

You are ready when you can explain the marker sections, produce a deliberate final file, and distinguish finishing from aborting.
