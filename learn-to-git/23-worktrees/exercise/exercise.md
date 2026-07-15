# Exercises: Work in Two Branches with Worktrees

Use a clean repository such as `pick-practice`.

## Exercise 1: Add a linked worktree

1. Confirm the main worktree is clean.
2. Add sibling worktree `pick-urgent` with new branch `urgent-fix` based on `main`.
3. List worktrees.
4. Enter the new directory and confirm its root and branch.

## Exercise 2: Share a commit, not working files

1. In `pick-urgent`, add and commit `urgent.txt`.
2. Return to the main worktree.
3. Confirm its working directory does not yet show `urgent.txt`.
4. Confirm its graph can already see `urgent-fix` and the commit.
5. Merge `urgent-fix` into `main` and confirm the file appears.

## Exercise 3: Remove cleanly

1. Confirm the linked worktree is clean.
2. From the main worktree, remove the linked worktree with Git.
3. List worktrees to verify removal.
4. Delete the merged `urgent-fix` branch with safe deletion.
