# Exercise Solutions: Resolve Merge Conflicts

## Exercise 1

```text
mkdir conflict-practice
cd conflict-practice
git init
git add color.txt
git commit -m "Add favorite color"
git switch -c choose-green
git add color.txt
git commit -m "Choose green"
git switch main
git add color.txt
git commit -m "Choose red"
git log --graph --oneline --decorate --all
git merge choose-green
```

Edit `color.txt` before each related add command. The merge should stop with a content conflict.

## Exercise 2

```text
git status
git diff
git merge --abort
git status
```

The top marker section was the red `main` content. The bottom was the green incoming content. After aborting, the file should say red.

## Exercise 3

```text
git merge choose-green
git add color.txt
git status
git diff --staged
git commit -m "Merge color choices as purple"
git log --graph --oneline --decorate --all
```

Edit the file to contain only `Color: purple` before `git add`. The graph should show a merge commit with two parents.
