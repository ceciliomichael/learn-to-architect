# Exercise Solutions: Revert Published Commits

## Exercise 1

```text
mkdir revert-practice
cd revert-practice
git init
git add settings.txt
git commit -m "Add safe settings"
git add settings.txt
git commit -m "Enable unsafe mode"
git add settings.txt
git commit -m "Add settings owner"
git log --oneline
```

Edit `settings.txt` to the stated content before each related add command.

## Exercise 2

Copy the hash from the log:

```text
git show UNSAFE_HASH
git revert UNSAFE_HASH
git status
git log --oneline
git show HEAD
```

The inverse patch should restore safe mode without removing the later owner line.

## Exercise 3

```text
git revert HEAD
git log --oneline
git show HEAD
```

Revert always adds normal history. The graph grows by two inverse decisions rather than deleting the original commits.
