# Exercise Solutions: Work in Two Branches with Worktrees

## Exercise 1

From the main worktree:

```text
git status
git worktree add -b urgent-fix ../pick-urgent main
git worktree list
cd ../pick-urgent
git rev-parse --show-toplevel
git branch --show-current
git status
```

## Exercise 2

In `pick-urgent`, after creating the file:

```text
git add urgent.txt
git commit -m "Add urgent fix note"
cd ../pick-practice
git status
git log --graph --oneline --decorate --all
git merge urgent-fix
```

Adjust the final path if your original repository folder has another name. The branch and commit are shared before merge, but the main working tree changes only when main moves.

## Exercise 3

```text
git -C ../pick-urgent status
git worktree remove ../pick-urgent
git worktree list
git branch -d urgent-fix
```

The linked directory should be gone and only the main worktree should remain listed.
